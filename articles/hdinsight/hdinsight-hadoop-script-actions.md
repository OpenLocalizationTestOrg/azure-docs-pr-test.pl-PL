---
title: "Skrypt programowanie akcji z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować klastry Hadoop za pomocą akcji skryptu. Akcja skryptu można zainstalować dodatkowe oprogramowanie uruchomione w klastrze Hadoop lub zmienić konfigurację aplikacji zainstalowany w klastrze."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 0e182e6b43fd2d17524c1da36cf4c204bb1b865a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="9c52f-104">Tworzenie skryptów akcji skryptu dla klastrów usługi HDInsight w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="9c52f-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="9c52f-105">Dowiedz się, jak napisać skrypty akcji skryptu dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c52f-105">Learn how to write Script Action scripts for HDInsight.</span></span> <span data-ttu-id="9c52f-106">Uzyskać informacji na temat używania skryptów akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="9c52f-107">Aby uzyskać ten sam artykuł, przeznaczony dla klastrów usługi HDInsight opartych na systemie Linux, zobacz [skryptów tworzenie akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-107">For the same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="9c52f-108">Kroki opisane w tym dokumencie działa tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="9c52f-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9c52f-109">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="9c52f-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="9c52f-110">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="9c52f-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9c52f-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="9c52f-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="9c52f-112">Uzyskać przy użyciu akcji skryptu z klastrów z systemem Linux, zobacz [programowanie akcji z usługą HDInsight (Linux) w skrypcie](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="9c52f-113">Akcja skryptu można zainstalować dodatkowe oprogramowanie uruchomione w klastrze Hadoop lub zmienić konfigurację aplikacji zainstalowany w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9c52f-113">Script Action can be used to install additional software running on a Hadoop cluster or to change the configuration of applications installed on a cluster.</span></span> <span data-ttu-id="9c52f-114">Akcje skryptu to skrypty uruchamiane w węzłach klastra, gdy klastry usługi HDInsight są wdrażane i są wykonywane po węzłów w klastrze Zakończ konfigurację usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c52f-114">Script actions are scripts that run on the cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in the cluster complete HDInsight configuration.</span></span> <span data-ttu-id="9c52f-115">Akcja skryptu jest wykonywane w ramach uprawnień konta administratora systemu i zapewnia pełne prawa dostępu do węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-115">A script action is executed under system admin account privileges and provides full access rights to the cluster nodes.</span></span> <span data-ttu-id="9c52f-116">Każdy klaster można podać listę akcji skryptu do wykonania w kolejności, w jakiej zostały określone.</span><span class="sxs-lookup"><span data-stu-id="9c52f-116">Each cluster can be provided with a list of script actions to be executed in the order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="9c52f-117">Jeśli wystąpi następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="9c52f-117">If you experience the following error message:</span></span>
>
> <span data-ttu-id="9c52f-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage: Termin "Zapisz HDIFile" nie został rozpoznany jako nazwa polecenia cmdlet, funkcji, pliku skryptu lub program wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="9c52f-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : The term 'Save-HDIFile' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="9c52f-119">Sprawdź pisownię nazwy lub jeśli ścieżki został uwzględniony, sprawdź, czy ścieżka jest poprawna i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="9c52f-119">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>
> <span data-ttu-id="9c52f-120">Jest on, ponieważ nie włączono metody pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="9c52f-120">It is because you didn't include the helper methods.</span></span>  <span data-ttu-id="9c52f-121">Zobacz [metody pomocnicze dla niestandardowych skryptów](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span><span class="sxs-lookup"><span data-stu-id="9c52f-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="9c52f-122">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="9c52f-122">Sample scripts</span></span>
<span data-ttu-id="9c52f-123">Do tworzenia klastrów usługi HDInsight w systemie operacyjnym Windows, akcja skryptu jest skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c52f-123">For creating HDInsight clusters on Windows operating system, the Script Action is Azure PowerShell script.</span></span> <span data-ttu-id="9c52f-124">Poniższy skrypt to przykład dla konfigurowania plików konfiguracji lokacji:</span><span class="sxs-lookup"><span data-stu-id="9c52f-124">The following script is a sample for configuring the site configuration files:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable to configure $ConfigFileName because it is not part of the HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

<span data-ttu-id="9c52f-125">Skrypt przyjmuje cztery parametry, nazwę pliku konfiguracji, właściwości, aby zmodyfikować wartość, którą chcesz skonfigurować oraz opis.</span><span class="sxs-lookup"><span data-stu-id="9c52f-125">The script takes four parameters, the configuration file name, the property you want to modify, the value you want to set, and a description.</span></span> <span data-ttu-id="9c52f-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9c52f-126">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="9c52f-127">Te parametry ustawia wartość hive.metastore.client.socket.timeout 90 w pliku gałęzi site.xml.</span><span class="sxs-lookup"><span data-stu-id="9c52f-127">These parameters sets the hive.metastore.client.socket.timeout value to 90 in the hive-site.xml file.</span></span>  <span data-ttu-id="9c52f-128">Wartość domyślna to 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="9c52f-128">The default value is 60 seconds.</span></span>

<span data-ttu-id="9c52f-129">Ten przykładowy skrypt można znaleźć w [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span><span class="sxs-lookup"><span data-stu-id="9c52f-129">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="9c52f-130">Usługa HDInsight zapewnia kilka skryptów do instalowania dodatkowych składników w klastrach HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9c52f-130">HDInsight provides several scripts to install additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="9c52f-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9c52f-131">Name</span></span> | <span data-ttu-id="9c52f-132">Skrypt</span><span class="sxs-lookup"><span data-stu-id="9c52f-132">Script</span></span> |
| --- | --- |
| <span data-ttu-id="9c52f-133">**Zainstaluj Spark**</span><span class="sxs-lookup"><span data-stu-id="9c52f-133">**Install Spark**</span></span> |<span data-ttu-id="9c52f-134">https://hdiconfigactions.blob.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c52f-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="9c52f-135">Zobacz [instalacji i używania platformy Spark w usłudze HDInsight clusters][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="9c52f-135">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="9c52f-136">**Zainstalować język R**</span><span class="sxs-lookup"><span data-stu-id="9c52f-136">**Install R**</span></span> |<span data-ttu-id="9c52f-137">https://hdiconfigactions.blob.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c52f-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="9c52f-138">Zobacz [instalacji i używania R w klastrach HDInsight][hdinsight-r-scripts].</span><span class="sxs-lookup"><span data-stu-id="9c52f-138">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="9c52f-139">**Zainstaluj Solr**</span><span class="sxs-lookup"><span data-stu-id="9c52f-139">**Install Solr**</span></span> |<span data-ttu-id="9c52f-140">https://hdiconfigactions.blob.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c52f-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="9c52f-141">Zobacz [instalacji i używania Solr w usłudze HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-141">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="9c52f-142">- **Zainstaluj Giraph**</span><span class="sxs-lookup"><span data-stu-id="9c52f-142">- **Install Giraph**</span></span> |<span data-ttu-id="9c52f-143">https://hdiconfigactions.blob.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c52f-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="9c52f-144">Zobacz [instalacji i używania Giraph w usłudze HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-144">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="9c52f-145">Akcja skryptu można wdrożyć przy użyciu portalu Azure, programu Azure PowerShell lub przy użyciu zestawu .NET SDK usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c52f-145">Script Action can be deployed from the Azure portal, Azure PowerShell or by using the HDInsight .NET SDK.</span></span>  <span data-ttu-id="9c52f-146">Aby uzyskać więcej informacji, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu][hdinsight-cluster-customize].</span><span class="sxs-lookup"><span data-stu-id="9c52f-146">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="9c52f-147">Przykładowe skrypty działa tylko z klastra usługi HDInsight w wersji 3.1 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="9c52f-147">The sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="9c52f-148">Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-148">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="9c52f-149">Metody pomocnicze dla niestandardowych skryptów</span><span class="sxs-lookup"><span data-stu-id="9c52f-149">Helper methods for custom scripts</span></span>
<span data-ttu-id="9c52f-150">Metody pomocnicze akcji skryptu są narzędzia, które można użyć podczas pisania skryptów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="9c52f-150">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="9c52f-151">Te metody są zdefiniowane w [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)i może być uwzględniony w skryptach przy użyciu poniższego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9c52f-151">These methods are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using the following sample:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module to make writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed to load HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="9c52f-152">Poniżej przedstawiono metody pomocnicze, które są udostępniane przez ten skrypt:</span><span class="sxs-lookup"><span data-stu-id="9c52f-152">Here are the helper methods that are provided by this script:</span></span>

| <span data-ttu-id="9c52f-153">Metoda pomocnika</span><span class="sxs-lookup"><span data-stu-id="9c52f-153">Helper method</span></span> | <span data-ttu-id="9c52f-154">Opis</span><span class="sxs-lookup"><span data-stu-id="9c52f-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c52f-155">**Zapisz HDIFile**</span><span class="sxs-lookup"><span data-stu-id="9c52f-155">**Save-HDIFile**</span></span> |<span data-ttu-id="9c52f-156">Pobierz plik z określonego identyfikatora URI (Uniform Resource) do lokalizacji na dysku lokalnym, który jest skojarzony z węzłem maszyny Wirtualnej Azure przypisana do klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-156">Download a file from the specified Uniform Resource Identifier (URI) to a location on the local disk that is associated with the Azure VM node assigned to the cluster.</span></span> |
| <span data-ttu-id="9c52f-157">**Rozwiń węzeł HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="9c52f-157">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="9c52f-158">Rozpakuj plik z rozszerzeniem zip.</span><span class="sxs-lookup"><span data-stu-id="9c52f-158">Unzip a zipped file.</span></span> |
| <span data-ttu-id="9c52f-159">**Wywołanie HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="9c52f-159">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="9c52f-160">Uruchom skrypt z cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="9c52f-160">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="9c52f-161">**HDILog zapisu**</span><span class="sxs-lookup"><span data-stu-id="9c52f-161">**Write-HDILog**</span></span> |<span data-ttu-id="9c52f-162">Zapisywania danych wyjściowych skryptu niestandardowego używanych w przypadku akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="9c52f-162">Write output from the custom script used for a script action.</span></span> |
| <span data-ttu-id="9c52f-163">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="9c52f-163">**Get-Services**</span></span> |<span data-ttu-id="9c52f-164">Pobierz listę usług uruchomionych na komputerze, w którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-164">Get a list of services running on the machine where the script executes.</span></span> |
| <span data-ttu-id="9c52f-165">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="9c52f-165">**Get-Service**</span></span> |<span data-ttu-id="9c52f-166">Przy użyciu nazwy określonej usługi jako dane wejściowe, uzyskać szczegółowe informacje dla określonej usługi (nazwy usługi, przetworzyć identyfikator, stan, itp.) na komputerze, na którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-166">With the specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="9c52f-167">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="9c52f-167">**Get-HDIServices**</span></span> |<span data-ttu-id="9c52f-168">Pobierz listę uruchomionych na komputerze, w którym skrypt jest wykonywany usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c52f-168">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c52f-169">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="9c52f-169">**Get-HDIService**</span></span> |<span data-ttu-id="9c52f-170">O określonej nazwie usługi HDInsight jako dane wejściowe, uzyskać szczegółowe informacje dla określonej usługi (nazwy usługi, przetworzyć identyfikator, stan, itp.) na komputerze, na którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-170">With the specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="9c52f-171">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="9c52f-171">**Get-ServicesRunning**</span></span> |<span data-ttu-id="9c52f-172">Pobierz listę usług, które są uruchomione na komputerze, na którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-172">Get a list of services that are running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c52f-173">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="9c52f-173">**Get-ServiceRunning**</span></span> |<span data-ttu-id="9c52f-174">Sprawdź, czy określonej usługi (według nazwy) działa na komputerze, którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-174">Check if a specific service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c52f-175">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="9c52f-175">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="9c52f-176">Pobierz listę uruchomionych na komputerze, w którym skrypt jest wykonywany usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c52f-176">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c52f-177">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="9c52f-177">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="9c52f-178">Sprawdź, czy określonej usługi HDInsight (według nazwy) działa na komputerze, którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-178">Check if a specific HDInsight service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c52f-179">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="9c52f-179">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="9c52f-180">Pobierz wersję platformy Hadoop zainstalowany na komputerze, na którym skrypt jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-180">Get the version of Hadoop installed on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c52f-181">**IsHDIHeadNode testu**</span><span class="sxs-lookup"><span data-stu-id="9c52f-181">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="9c52f-182">Sprawdź, czy komputer, na którym skrypt jest wykonywany jest węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="9c52f-182">Check if the computer where the script executes is a head node.</span></span> |
| <span data-ttu-id="9c52f-183">**IsActiveHDIHeadNode testu**</span><span class="sxs-lookup"><span data-stu-id="9c52f-183">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="9c52f-184">Sprawdź, czy komputer, na którym skrypt jest wykonywany jest aktywnego węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="9c52f-184">Check if the computer where the script executes is an active head node.</span></span> |
| <span data-ttu-id="9c52f-185">**IsHDIDataNode testu**</span><span class="sxs-lookup"><span data-stu-id="9c52f-185">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="9c52f-186">Sprawdź, czy komputer, na którym skrypt jest wykonywany jest węzeł danych.</span><span class="sxs-lookup"><span data-stu-id="9c52f-186">Check if the computer where the script executes is a data node.</span></span> |
| <span data-ttu-id="9c52f-187">**Edytuj HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="9c52f-187">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="9c52f-188">Edytuj pliki konfiguracji hive-site.xml, core-site.xml, system plików hdfs-site.xml, mapred-site.xml lub yarn-site.xml.</span><span class="sxs-lookup"><span data-stu-id="9c52f-188">Edit the config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="9c52f-189">Najlepsze rozwiązania dotyczące tworzenia skryptów</span><span class="sxs-lookup"><span data-stu-id="9c52f-189">Best practices for script development</span></span>
<span data-ttu-id="9c52f-190">Podczas opracowywania niestandardowego skryptu dla klastra usługi HDInsight, istnieje kilka najlepszych rozwiązań, które należy wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="9c52f-190">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* <span data-ttu-id="9c52f-191">Sprawdź, czy wersja usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="9c52f-191">Check for the Hadoop version</span></span>

    <span data-ttu-id="9c52f-192">HDInsight w wersji 3.1 (Hadoop 2.4) lub nowszym pomocy technicznej, aby zainstalować składniki niestandardowe w klastrze za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="9c52f-192">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action to install custom components on a cluster.</span></span> <span data-ttu-id="9c52f-193">W skrypcie niestandardowe, należy użyć **Get HDIHadoopVersion** metody pomocniczej, aby sprawdzić wersję platformy Hadoop, przed kontynuowaniem wykonywania innych zadań w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="9c52f-193">In your custom script, you must use the **Get-HDIHadoopVersion** helper method to check the Hadoop version before proceeding with performing other tasks in the script.</span></span>
* <span data-ttu-id="9c52f-194">Podaj stabilna linki do zasobów skryptu</span><span class="sxs-lookup"><span data-stu-id="9c52f-194">Provide stable links to script resources</span></span>

    <span data-ttu-id="9c52f-195">Użytkownicy upewnij się, że wszystkie skrypty i inne artefaktów używane w dostosowania klastra nadal dostępne w okresie istnienia klastra i wersje tych plików nie należy zmieniać na czas trwania.</span><span class="sxs-lookup"><span data-stu-id="9c52f-195">Users should make sure that all the scripts and other artifacts used in the customization of a cluster remain available throughout the lifetime of the cluster and that the versions of these files do not change for the duration.</span></span> <span data-ttu-id="9c52f-196">Te zasoby są wymagane, jeśli wymagana jest ponownym węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9c52f-196">These resources are required if the reimaging of nodes in the cluster is required.</span></span> <span data-ttu-id="9c52f-197">Najlepszym rozwiązaniem jest pobrać i zarchiwizowanie wszystkich na koncie magazynu, która kontroluje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c52f-197">The best practice is to download and archive everything in a Storage account that the user controls.</span></span> <span data-ttu-id="9c52f-198">Może to być domyślne konto magazynu ani żadnych dodatkowych kont magazynu określony w czasie wdrażania dostosowanego klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-198">This can be the default Storage account or any of the additional Storage accounts specified at the time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="9c52f-199">Spark i R dostosowane klastra przykłady podane w dokumentacji, na przykład wprowadzono lokalną kopię zasoby na tym koncie magazynu: https://hdiconfigactions.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="9c52f-199">In the Spark and R customized cluster samples provided in the documentation, for example, we have made a local copy of the resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="9c52f-200">Upewnij się, że skrypt dostosowywania klastra jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="9c52f-200">Ensure that the cluster customization script is idempotent</span></span>

    <span data-ttu-id="9c52f-201">Należy oczekiwać, że węzły klastra usługi HDInsight zostanie odtworzone z obrazu okres istnienia klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-201">You must expect that the nodes of an HDInsight cluster is reimaged during the cluster lifetime.</span></span> <span data-ttu-id="9c52f-202">Skrypt dostosowywania klastra jest uruchamiane przy każdym klastrze zostanie odtworzone z obrazu.</span><span class="sxs-lookup"><span data-stu-id="9c52f-202">The cluster customization script is run whenever a cluster is reimaged.</span></span> <span data-ttu-id="9c52f-203">Ten skrypt muszą być zaprojektowane jako idempotentności w tym sensie, że po ponownej instalacji systemu, skrypt należy upewnij się, że klaster jest zwracana do tej samej dostosowywać stan, który znajdował się tuż po skrypt został uruchomiony po raz pierwszy, gdy klaster został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9c52f-203">This script must be designed to be idempotent in the sense that upon reimaging, the script should ensure that the cluster is returned to the same customized state that it was in just after the script ran for the first time when the cluster was initially created.</span></span> <span data-ttu-id="9c52f-204">Na przykład, jeżeli skryptu niestandardowego zainstalować aplikację na D:\AppLocation przy pierwszym uruchomieniu, następnie przy każdym uruchomieniu kolejne, po ponownym, skrypt należy sprawdzić, czy aplikacja znajduje się w lokalizacji D:\AppLocation przed kontynuowaniem z innymi kroki opisane w temacie skrypt.</span><span class="sxs-lookup"><span data-stu-id="9c52f-204">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon reimaging, the script should check whether the application exists at the D:\AppLocation location before proceeding with other steps in the script.</span></span>
* <span data-ttu-id="9c52f-205">Zainstaluj składniki niestandardowe w optymalny lokalizacji</span><span class="sxs-lookup"><span data-stu-id="9c52f-205">Install custom components in the optimal location</span></span>

    <span data-ttu-id="9c52f-206">Jeśli węzły klastra są odtworzyć z obrazu, dysku C:\ zasobów i dysku D:\ system można ponownie sformatowany, co grozi utratą danych i aplikacji, które były zainstalowane na tych dyskach.</span><span class="sxs-lookup"><span data-stu-id="9c52f-206">When cluster nodes are reimaged, the C:\ resource drive and D:\ system drive can be reformatted, resulting in the loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="9c52f-207">Może to również nastąpić, jeśli węzeł maszyny wirtualnej platformy Azure (VM), który jest częścią klastra ulegnie awarii i zostało zastąpione przez nowy węzeł.</span><span class="sxs-lookup"><span data-stu-id="9c52f-207">This could also happen if an Azure virtual machine (VM) node that is part of the cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="9c52f-208">Składniki można zainstalować na dysku D:\, lub w lokalizacji C:\apps w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9c52f-208">You can install components on the D:\ drive or in the C:\apps location on the cluster.</span></span> <span data-ttu-id="9c52f-209">Wszystkich innych lokalizacji na dysku C:\ są zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="9c52f-209">All other locations on the C:\ drive are reserved.</span></span> <span data-ttu-id="9c52f-210">Określ lokalizację, w których aplikacje lub biblioteki ma być zainstalowany w klastrze dostosowywania skryptu.</span><span class="sxs-lookup"><span data-stu-id="9c52f-210">Specify the location where applications or libraries are to be installed in the cluster customization script.</span></span>
* <span data-ttu-id="9c52f-211">Zapewni to wysoką dostępność architektury klastra</span><span class="sxs-lookup"><span data-stu-id="9c52f-211">Ensure high availability of the cluster architecture</span></span>

    <span data-ttu-id="9c52f-212">HDInsight ma architekturę aktywny / pasywny wysokiej dostępności, jednego z węzła głównego w trybie aktywnym (w którym są uruchomione usługi HDInsight) i innych węzła głównego jest w trybie rezerwy (w którym HDInsight usługi nie działają).</span><span class="sxs-lookup"><span data-stu-id="9c52f-212">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where the HDInsight services are running) and the other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="9c52f-213">Węzły przełącznika tryby aktywnym i pasywnym, jeśli usługi HDInsight są przerywane.</span><span class="sxs-lookup"><span data-stu-id="9c52f-213">The nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="9c52f-214">Jeśli akcja skryptu jest używany do instalowania usług na obu węzłach głównych wysokiej dostępności, należy pamiętać, mechanizm pracy awaryjnej usługi HDInsight nie jest automatycznie awaryjnie tych usług zainstalowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c52f-214">If a script action is used to install services on both head nodes for high availability, note that the HDInsight failover mechanism is not able to automatically fail over these user-installed services.</span></span> <span data-ttu-id="9c52f-215">Dlatego użytkownik zainstalował usług na HDInsight węzłów głównych, które powinny być wysokiej dostępności musisz mieć własne mechanizm pracy awaryjnej w trybie aktywny / pasywny lub być w trybie aktywny / aktywny.</span><span class="sxs-lookup"><span data-stu-id="9c52f-215">So user-installed services on HDInsight head nodes that are expected to be highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="9c52f-216">Akcja skryptu HDInsight polecenie jest uruchamiane na obu węzłach głównych, gdy rola head węzła jest określony jako wartość *ClusterRoleCollection* parametru.</span><span class="sxs-lookup"><span data-stu-id="9c52f-216">An HDInsight Script Action command runs on both head nodes when the head-node role is specified as a value in the *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="9c52f-217">Tak podczas projektowania niestandardowego skryptu, upewnij się, że skrypt jest świadome tego Instalatora.</span><span class="sxs-lookup"><span data-stu-id="9c52f-217">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="9c52f-218">Nie należy uruchamiać do problemów, gdy te same usługi są zainstalowane i uruchomione na obu węzłów głównych i ich przechodzili konkurujących ze sobą.</span><span class="sxs-lookup"><span data-stu-id="9c52f-218">You should not run into problems where the same services are installed and started on both of the head nodes and they end up competing with each other.</span></span> <span data-ttu-id="9c52f-219">Pamiętaj też, że dane zostały utracone podczas ponownej instalacji systemu, więc oprogramowania zainstalowanych za pomocą akcji skryptu musi być odporny na takie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9c52f-219">Also, be aware that data is lost during reimaging, so software installed via Script Action has to be resilient to such events.</span></span> <span data-ttu-id="9c52f-220">Aplikacje powinny zaprojektowane w taki sposób, aby pracować z danymi wysokiej dostępności, która jest dystrybuowana do wielu węzłów.</span><span class="sxs-lookup"><span data-stu-id="9c52f-220">Applications should be designed to work with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="9c52f-221">Należy pamiętać, że maksymalnie 1/5 węzłów w klastrze mogą można odtworzyć z obrazu w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="9c52f-221">Note that as many as 1/5 of the nodes in a cluster can be reimaged at the same time.</span></span>
* <span data-ttu-id="9c52f-222">Konfigurowanie niestandardowych składników można używać magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c52f-222">Configure the custom components to use Azure Blob storage</span></span>

    <span data-ttu-id="9c52f-223">Niestandardowych składników, które należy zainstalować na węzłach klastra może być domyślna konfiguracja korzystania z magazynu systemu Distributed plików Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="9c52f-223">The custom components that you install on the cluster nodes might have a default configuration to use Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="9c52f-224">Należy zmienić konfigurację, aby zamiast tego użyj magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c52f-224">You should change the configuration to use Azure Blob storage instead.</span></span> <span data-ttu-id="9c52f-225">Na odtworzenia z obrazu klastra sformatowany pobiera system plików HDFS i zostaną utracone wszystkie dane są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="9c52f-225">On a cluster reimage, the HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="9c52f-226">Zamiast tego przy użyciu magazynu obiektów Blob platformy Azure zapewnia, że dane są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="9c52f-226">Using Azure Blob storage instead ensures that your data is retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="9c52f-227">Wspólne wzorce użycia</span><span class="sxs-lookup"><span data-stu-id="9c52f-227">Common usage patterns</span></span>
<span data-ttu-id="9c52f-228">Ta sekcja zawiera wskazówki dotyczące implementowania niektóre typowe wzorce użycia, które możesz napotkać podczas pisania skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="9c52f-228">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="9c52f-229">Skonfiguruj zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="9c52f-229">Configure environment variables</span></span>
<span data-ttu-id="9c52f-230">Często w rozwoju akcji skryptu, uważasz, że trzeba ustawić zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="9c52f-230">Often in script action development, you feel the need to set environment variables.</span></span> <span data-ttu-id="9c52f-231">Na przykład najbardziej prawdopodobnym scenariuszem jest podczas pobierania pliku binarnego z zewnętrznej witryny, zainstaluj go w klastrze i Dodaj lokalizację miejsca do Twojej zmiennej środowiskowej "PATH", w którym jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-231">For instance, a most likely scenario is when you download a binary from an external site, install it on the cluster, and add the location of where it is installed to your ‘PATH’ environment variable.</span></span> <span data-ttu-id="9c52f-232">Poniższy fragment kodu pokazano, jak ustawić zmienne środowiskowe w skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="9c52f-232">The following snippet shows you how to set environment variables in the custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="9c52f-233">Ta instrukcja ustawia zmienną środowiskową **MDS_RUNNER_CUSTOM_CLUSTER** na wartość "true", a także ustawia zakres tej zmiennej jako komputera.</span><span class="sxs-lookup"><span data-stu-id="9c52f-233">This statement sets the environment variable **MDS_RUNNER_CUSTOM_CLUSTER** to the value 'true' and also sets the scope of this variable to be machine-wide.</span></span> <span data-ttu-id="9c52f-234">W czasie ważne jest, że zmienne środowiskowe są ustawiane na odpowiedni zakres — komputera lub użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c52f-234">At times it is important that environment variables are set at the appropriate scope – machine or user.</span></span> <span data-ttu-id="9c52f-235">Zobacz [tutaj] [ 1] Aby uzyskać więcej informacji na temat ustawiania zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="9c52f-235">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="9c52f-236">Dostęp do lokalizacji, w którym są przechowywane niestandardowe skrypty</span><span class="sxs-lookup"><span data-stu-id="9c52f-236">Access to locations where the custom scripts are stored</span></span>
<span data-ttu-id="9c52f-237">Skrypty używane w celu dostosowania klastra musi być albo w domyślne konto magazynu dla klastra lub w publicznego kontenera tylko do odczytu na inne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c52f-237">Scripts used to customize a cluster needs to either be in the default storage account for the cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="9c52f-238">Jeśli skrypt uzyskuje dostęp do zasobów znajdujących się w innym miejscu te muszą być publicznie dostępny (co najmniej publiczne tylko do odczytu).</span><span class="sxs-lookup"><span data-stu-id="9c52f-238">If your script accesses resources located elsewhere these need to be in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="9c52f-239">Na przykład można uzyskać dostępu do pliku i zapisz go przy użyciu polecenia SaveFile HDI.</span><span class="sxs-lookup"><span data-stu-id="9c52f-239">For instance you might want to access a file and save it using the SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="9c52f-240">W tym przykładzie należy się upewnić, że kontener "somecontainer" na koncie magazynu "somestorageaccount" jest dostępny publicznie.</span><span class="sxs-lookup"><span data-stu-id="9c52f-240">In this example, you must ensure that the container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="9c52f-241">W przeciwnym razie skrypt zgłasza wyjątek nie znaleziono i zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9c52f-241">Otherwise, the script throws a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-to-the-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="9c52f-242">Przekazania parametrów do polecenia cmdlet Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="9c52f-242">Pass parameters to the Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="9c52f-243">Aby przekazać wiele parametrów polecenia cmdlet Add-AzureRmHDInsightScriptAction, należy sformatować wartość ciągu zawiera wszystkie parametry skryptu.</span><span class="sxs-lookup"><span data-stu-id="9c52f-243">To pass multiple parameters to the Add-AzureRmHDInsightScriptAction cmdlet, you need to format the string value to contain all parameters for the script.</span></span> <span data-ttu-id="9c52f-244">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9c52f-244">For example:</span></span>

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="9c52f-245">lub</span><span class="sxs-lookup"><span data-stu-id="9c52f-245">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="9c52f-246">Zgłoszenie wyjątku dla wdrożenia klastra nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="9c52f-246">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="9c52f-247">Aby dokładnie bądź na bieżąco z faktu, że klaster dostosowanie nie powiodło się zgodnie z oczekiwaniami, ważne jest, aby zgłosić wyjątek, niepowodzeniem tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-247">If you want to get accurately notified of the fact that cluster customization did not succeed as expected, it is important to throw an exception and fail the cluster creation.</span></span> <span data-ttu-id="9c52f-248">Na przykład można przetworzyć pliku, jeśli istnieje i obsługę w przypadku błędu, gdy plik nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="9c52f-248">For instance, you might want to process a file if it exists and handle the error case where the file does not exist.</span></span> <span data-ttu-id="9c52f-249">Może to zapewnić skrypt zakończy pracę bezpiecznie i stan klastra jest poprawnie znany.</span><span class="sxs-lookup"><span data-stu-id="9c52f-249">This would ensure that the script exits gracefully and the state of the cluster is correctly known.</span></span> <span data-ttu-id="9c52f-250">Poniższy fragment kodu przedstawiono przykładowy sposób można to osiągnąć:</span><span class="sxs-lookup"><span data-stu-id="9c52f-250">The following snippet gives an example of how to achieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="9c52f-251">W tym fragmencie Jeśli plik nie istnieje, spowodowałoby to stan, w którym skrypt faktycznie opuszcza bezpiecznie po wydrukowaniu komunikat o błędzie, a klastra osiągnie uruchomiona przy założeniu, że "pomyślnie" ukończyć procesu dostosowywania klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-251">In this snippet, if the file did not exist, it would lead to a state where the script actually exits gracefully after printing the error message, and the cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="9c52f-252">Aby dokładnie powiadamianych fakt, że klaster dostosowania zasadniczo nie powiodło się zgodnie z oczekiwaniami ze względu na Brak pliku, więcej należy zgłosić wyjątek, niepowodzeniem, krok dostosowania klastra.</span><span class="sxs-lookup"><span data-stu-id="9c52f-252">If you want to be accurately notified of the fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate to throw an exception and fail the cluster customization step.</span></span> <span data-ttu-id="9c52f-253">Aby to zrobić, należy użyć poniższy fragment kodu przykładowej zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="9c52f-253">To achieve this you must use the following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="9c52f-254">Lista kontrolna wdrażania akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="9c52f-254">Checklist for deploying a script action</span></span>
<span data-ttu-id="9c52f-255">Poniżej przedstawiono kroki, które Wybraliśmy podczas przygotowania do wdrożenia tych skryptów:</span><span class="sxs-lookup"><span data-stu-id="9c52f-255">Here are the steps we took when preparing to deploy these scripts:</span></span>

1. <span data-ttu-id="9c52f-256">Umieścić pliki, które zawierają niestandardowe skrypty w miejscu, który jest dostępny dla węzłów klastra podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9c52f-256">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="9c52f-257">Może to być domyślne lub dodatkowych kont magazynu określony w czasie wdrażania klastra lub innych kontenera magazynu publicznie.</span><span class="sxs-lookup"><span data-stu-id="9c52f-257">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="9c52f-258">Dodaj kontroli w skryptach, aby upewnić się, że są one wykonywane idempotently, dzięki czemu skrypt mogą być wykonywane wiele razy w tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="9c52f-258">Add checks into scripts to make sure that they execute idempotently, so that the script can be executed multiple times on the same node.</span></span>
3. <span data-ttu-id="9c52f-259">Użyj **Write-Output** polecenia cmdlet programu Azure PowerShell do drukowania do STDOUT, a także STDERR.</span><span class="sxs-lookup"><span data-stu-id="9c52f-259">Use the **Write-Output** Azure PowerShell cmdlet to print to STDOUT as well as STDERR.</span></span> <span data-ttu-id="9c52f-260">Nie używaj **Write-Host**.</span><span class="sxs-lookup"><span data-stu-id="9c52f-260">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="9c52f-261">Użyj folder plików tymczasowych, takich jak $env: TEMP, aby zachować pobrany plik używany przez skrypty i następnie wyczyść je po wykonaniu skryptów.</span><span class="sxs-lookup"><span data-stu-id="9c52f-261">Use a temporary file folder, such as $env:TEMP, to keep the downloaded file used by the scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="9c52f-262">Zainstaluj oprogramowanie niestandardowe tylko na D:\ lub C:\apps.</span><span class="sxs-lookup"><span data-stu-id="9c52f-262">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="9c52f-263">Są one zastrzeżone nie należy używać innych lokalizacji na dysku C:.</span><span class="sxs-lookup"><span data-stu-id="9c52f-263">Other locations on the C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="9c52f-264">Należy pamiętać, że instalowanie plików na dysku C: poza folderem C:\apps może spowodować błędy instalacji podczas reimages węzła.</span><span class="sxs-lookup"><span data-stu-id="9c52f-264">Note that installing files on the C: drive outside of the C:\apps folder may result in setup failures during reimages of the node.</span></span>
6. <span data-ttu-id="9c52f-265">W przypadku, gdy zmieniono ustawienia na poziomie systemu operacyjnego lub plików konfiguracyjnych usługi Hadoop, możesz ponownie uruchomić usługi HDInsight, dzięki czemu mogą one odbierać wszystkie ustawienia poziomu systemu operacyjnego, takich jak zmiennych środowiskowych w skryptach.</span><span class="sxs-lookup"><span data-stu-id="9c52f-265">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="9c52f-266">Debugowanie skryptów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="9c52f-266">Debug custom scripts</span></span>
<span data-ttu-id="9c52f-267">Dzienniki błędów skryptów są przechowywane wraz z innymi dane wyjściowe w domyślne konto magazynu określone dla klastra podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="9c52f-267">The script error logs are stored, along with other output, in the default Storage account that you specified for the cluster at its creation.</span></span> <span data-ttu-id="9c52f-268">Dzienniki są przechowywane w tabeli o nazwie *u < \cluster-name-fragment >< \time-stamp > setuplog*.</span><span class="sxs-lookup"><span data-stu-id="9c52f-268">The logs are stored in a table with the name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="9c52f-269">Są to dzienniki zagregowane, które rekordy z wszystkie węzły (węzła głównego i węzły procesów roboczych), na których skrypt jest uruchamiany w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9c52f-269">These are aggregated logs that have records from all of the nodes (head node and worker nodes) on which the script runs in the cluster.</span></span>
<span data-ttu-id="9c52f-270">Jest łatwy sposób Sprawdź dzienniki do użycia narzędzi HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c52f-270">An easy way to check the logs is to use HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="9c52f-271">Dla instalacji narzędzi, zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="9c52f-271">For installing the tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="9c52f-272">**Aby sprawdzić dziennika za pomocą programu Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9c52f-272">**To check the log using Visual Studio**</span></span>

1. <span data-ttu-id="9c52f-273">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c52f-273">Open Visual Studio.</span></span>
2. <span data-ttu-id="9c52f-274">Kliknij przycisk **widoku**, a następnie kliknij przycisk **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="9c52f-274">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="9c52f-275">Kliknij prawym przyciskiem myszy "Azure", kliknij przycisk Połącz z **subskrypcji platformy Microsoft Azure**, a następnie wprowadź swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="9c52f-275">Right-click "Azure", click Connect to **Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="9c52f-276">Rozwiń węzeł **magazynu**, rozwiń konto magazynu Azure używany jako domyślny system plików, rozwiń **tabel**, a następnie kliknij dwukrotnie nazwę tabeli.</span><span class="sxs-lookup"><span data-stu-id="9c52f-276">Expand **Storage**, expand the Azure storage account used as the default file system, expand **Tables**, and then double-click the table name.</span></span>

<span data-ttu-id="9c52f-277">Można również zdalnego w węzłach klastra, aby wyświetlić zarówno STDOUT i STDERR niestandardowych skryptów.</span><span class="sxs-lookup"><span data-stu-id="9c52f-277">You can also remote into the cluster nodes to see both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="9c52f-278">Dzienniki w każdym węźle są specyficzne tylko dla tego węzła i logują się do **C:\HDInsightLogs\DeploymentAgent.log**.</span><span class="sxs-lookup"><span data-stu-id="9c52f-278">The logs on each node are specific only to that node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="9c52f-279">Te pliki dziennika rejestrować wszystkie dane wyjściowe skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="9c52f-279">These log files record all outputs from the custom script.</span></span> <span data-ttu-id="9c52f-280">Przykład fragment dziennika akcji skryptu Spark wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9c52f-280">An example log snippet for a Spark script action looks like this:</span></span>

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


<span data-ttu-id="9c52f-281">W tym dzienniku jest jasne, czy akcja skryptu Spark zostało wykonane na Maszynie wirtualnej o nazwie HEADNODE0 i że nie zwrócono wyjątek podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9c52f-281">In this log, it is clear that the Spark script action has been executed on the VM named HEADNODE0 and that no exceptions were thrown during the execution.</span></span>

<span data-ttu-id="9c52f-282">W przypadku, gdy wystąpi błąd wykonania, dane wyjściowe opisujące on również znajduje się w tym pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="9c52f-282">In the event that an execution failure occurs, the output describing it is also contained in this log file.</span></span> <span data-ttu-id="9c52f-283">Informacje zawarte w tych dziennikach powinna być pomocnych w debugowaniu problemów skryptu, które mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="9c52f-283">The information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="9c52f-284">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9c52f-284">See also</span></span>
* <span data-ttu-id="9c52f-285">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="9c52f-285">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="9c52f-286">[Zainstalować i używać platformy Spark w usłudze hdinsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="9c52f-286">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="9c52f-287">[Zainstaluj i użyj języka R w klastrach HDInsight][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="9c52f-287">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="9c52f-288">[Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-288">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="9c52f-289">[Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c52f-289">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
