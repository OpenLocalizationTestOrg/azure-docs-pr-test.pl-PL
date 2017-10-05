---
title: "Monitorowanie Maszynę wirtualną z rozszerzenia maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozszerzenie diagnostycznych Linux służy do monitorowania wydajności i danych diagnostycznych maszyny wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: b8c6e2e22d8478b6e92e7b7942f15d37a840fed3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-linux-diagnostic-extension-to-monitor-the-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="06b32-103">Używanie rozszerzenia diagnostycznego systemu Linux do monitorowania wydajności i danych diagnostycznych maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="06b32-103">Use the Linux Diagnostic Extension to monitor the performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="06b32-104">W tym dokumencie opisano wersji 2.3 rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="06b32-104">This document describes version 2.3 of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06b32-105">Ta wersja jest przestarzały i może być nieopublikowane dowolnym momencie po 30 czerwca 2018.</span><span class="sxs-lookup"><span data-stu-id="06b32-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="06b32-106">Zastąpiono wersji 3.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="06b32-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="06b32-107">Aby uzyskać więcej informacji, zobacz [dokumentację w wersji 3.0 rozszerzenia diagnostycznych Linux](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="06b32-107">For more information, see the [documentation for version 3.0 of the Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="06b32-108">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="06b32-108">Introduction</span></span>

<span data-ttu-id="06b32-109">(**Uwaga**: rozszerzenie diagnostyczne systemu Linux jest open-powierzając jej ich konserwację na [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) gdzie najbardziej aktualnych informacji o rozszerzeniu pierwszej publikacji.</span><span class="sxs-lookup"><span data-stu-id="06b32-109">(**Note**: The Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where the most current information on the extension is first published.</span></span> <span data-ttu-id="06b32-110">Należy sprawdzić [GitHub strony](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) pierwszej.)</span><span class="sxs-lookup"><span data-stu-id="06b32-110">You might want to check the [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="06b32-111">Rozszerzenie diagnostycznych Linux pomaga monitor użytkownika maszyn wirtualnych systemu Linux, które działają w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-111">The Linux Diagnostic Extension helps a user monitor the Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="06b32-112">Ma ona następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="06b32-112">It has the following capabilities:</span></span>

* <span data-ttu-id="06b32-113">Zbiera i przekazuje informacje o wydajności systemu z maszyny Wirtualnej systemu Linux do tabeli magazynu użytkownika, w tym informacji diagnostycznych i syslog.</span><span class="sxs-lookup"><span data-stu-id="06b32-113">Collects and uploads the system performance information from the Linux VM to the user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="06b32-114">Umożliwia dostosowanie metryk danych, które zostaną zebrane i przekazane.</span><span class="sxs-lookup"><span data-stu-id="06b32-114">Enables users to customize the data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="06b32-115">Umożliwia użytkownikom na przekazywanie do tabeli magazynu wyznaczonego określone pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="06b32-115">Enables users to upload specified log files to a designated storage table.</span></span>

<span data-ttu-id="06b32-116">W bieżącej wersji 2.3 dane obejmują:</span><span class="sxs-lookup"><span data-stu-id="06b32-116">In the current version 2.3, the data includes:</span></span>

* <span data-ttu-id="06b32-117">Wszystkie dzienniki Linux Rsyslog, w tym system, zabezpieczenia i dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="06b32-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="06b32-118">Wszystkie dane systemu, które jest określone w [lokacji rozwiązania Cross platformy w programie System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="06b32-118">All system data that's specified on [the System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="06b32-119">Pliki dziennika zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="06b32-119">User-specified log files.</span></span>

<span data-ttu-id="06b32-120">To rozszerzenie działa zarówno z klasycznego i modeli wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="06b32-120">This extension works with both the classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-the-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="06b32-121">Bieżąca wersja rozszerzenia i amortyzacja stare wersje</span><span class="sxs-lookup"><span data-stu-id="06b32-121">Current version of the extension and deprecation of old versions</span></span>

<span data-ttu-id="06b32-122">Najnowsza wersja rozszerzenia **2.3**, i **wszystkie starsze wersje (2.0, 2.1 i 2.2) zostanie zastąpiona i nieopublikowane końca roku (2017)**.</span><span class="sxs-lookup"><span data-stu-id="06b32-122">The latest version of the extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="06b32-123">Po zainstalowaniu rozszerzenia Diagnostyka systemu Linux wraz z uaktualnieniem automatyczne wersja pomocnicza wyłączone, zdecydowanie zaleca się odinstalować rozszerzenia, a następnie zainstaluj go ponownie z uaktualnieniem automatyczne wersja pomocnicza włączone.</span><span class="sxs-lookup"><span data-stu-id="06b32-123">If you installed the Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall the extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="06b32-124">W klasycznym (ASM) maszyn wirtualnych można to osiągnąć, określając "2.*" jako wersja instalowania rozszerzenia za pomocą interfejsu wiersza polecenia XPLAT platformy Azure lub programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="06b32-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="06b32-125">Na maszynach ARM można to osiągnąć poprzez włączenie ""autoUpgradeMinorVersion": true" w szablonie wdrożenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06b32-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span> <span data-ttu-id="06b32-126">Ponadto żadnej nowej instalacji rozszerzenia powinien mieć wersja pomocnicza automatycznego uaktualniania opcja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="06b32-126">Also, any new installation of the extension should have the auto minor version upgrade option turned on.</span></span>

## <a name="enable-the-extension"></a><span data-ttu-id="06b32-127">Włącz rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="06b32-127">Enable the extension</span></span>

<span data-ttu-id="06b32-128">To rozszerzenie można włączyć za pomocą [portalu Azure](https://portal.azure.com/#), programu Azure PowerShell lub skryptów wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-128">You can enable this extension by using the [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="06b32-129">Aby wyświetlić i skonfigurować wydajność systemu i dane bezpośrednio z portalu Azure, wykonaj [następujące kroki na blogu Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="06b32-129">To view and configure the system and performance data directly from the Azure portal, follow [these steps on the Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="06b32-130">W tym artykule przedstawiono sposób włączania i konfigurowania rozszerzenia przy użyciu poleceń wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-130">This article focuses on how to enable and configure the extension by using Azure CLI commands.</span></span> <span data-ttu-id="06b32-131">Dzięki temu można odczytać oraz jak wyświetlać dane bezpośrednio z tabeli magazynu.</span><span class="sxs-lookup"><span data-stu-id="06b32-131">This allows you to read and view the data directly from the storage table.</span></span>

<span data-ttu-id="06b32-132">Należy pamiętać, że metody konfiguracji, które zostały opisane w tym miejscu nie będzie działać dla portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-132">Note that the configuration methods that are described here won't work for the Azure portal.</span></span> <span data-ttu-id="06b32-133">Aby wyświetlić i skonfigurować wydajność systemu i dane bezpośrednio z portalu Azure, należy włączyć rozszerzenie za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="06b32-133">To view and configure the system and performance data directly from the Azure portal, the extension must be enabled through the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06b32-134">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="06b32-134">Prerequisites</span></span>

* <span data-ttu-id="06b32-135">**Agenta systemu Linux platformy Azure w wersji 2.0.6 lub nowszym**.</span><span class="sxs-lookup"><span data-stu-id="06b32-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="06b32-136">Należy pamiętać, że większość obrazów Galeria Linux maszyny Wirtualnej Azure obejmuje wersji 2.0.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="06b32-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="06b32-137">Można uruchomić **agenta WAAgent-wersja** o potwierdzenie, która wersja jest zainstalowana na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06b32-137">You can run **WAAgent -version** to confirm which version is installed on the VM.</span></span> <span data-ttu-id="06b32-138">Jeśli maszyna wirtualna działa w wersji starszej niż 2.0.6, można wykonać [tych instrukcji w serwisie GitHub](https://github.com/Azure/WALinuxAgent "instrukcje") go zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="06b32-138">If the VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") to update it.</span></span>
* <span data-ttu-id="06b32-139">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="06b32-139">**Azure CLI**.</span></span> <span data-ttu-id="06b32-140">Postępuj zgodnie z [tym instrukcje dotyczące instalowania interfejsu wiersza polecenia](../../../cli-install-nodejs.md) do skonfigurowania środowiska wiersza polecenia platformy Azure na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="06b32-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) to set up the Azure CLI environment on your machine.</span></span> <span data-ttu-id="06b32-141">Po zainstalowaniu interfejsu wiersza polecenia Azure, możesz użyć **azure** polecenie z interfejsu wiersza polecenia (Bash, Terminal lub wiersza polecenia) do poleceń wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-141">After Azure CLI is installed, you can use the **azure** command from your command-line interface (Bash, Terminal, or command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="06b32-142">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="06b32-142">For example:</span></span>

  * <span data-ttu-id="06b32-143">Uruchom **zestaw rozszerzenie azure maszyny wirtualnej — Pomoc** uzyskać szczegółową pomoc.</span><span class="sxs-lookup"><span data-stu-id="06b32-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="06b32-144">Uruchom **logowanie w usłudze azure** logować się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-144">Run **azure login** to sign in to Azure.</span></span>
  * <span data-ttu-id="06b32-145">Uruchom **listy maszyna wirtualna platformy azure** do tworzenia listy wszystkich maszyn wirtualnych, które masz na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-145">Run **azure vm list** to list all the virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="06b32-146">Konto magazynu do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="06b32-146">A storage account to store the data.</span></span> <span data-ttu-id="06b32-147">Konieczne będzie nazwa konta magazynu, które zostało utworzone wcześniej i klucza dostępu, aby przekazać dane do usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="06b32-147">You will need a storage account name that was created previously and an access key to upload the data to your storage.</span></span>

## <a name="use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension"></a><span data-ttu-id="06b32-148">Użyj polecenia interfejsu wiersza polecenia Azure, aby włączyć rozszerzenie diagnostyczne systemu Linux</span><span class="sxs-lookup"><span data-stu-id="06b32-148">Use the Azure CLI command to enable the Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-the-extension-with-the-default-data-set"></a><span data-ttu-id="06b32-149">Scenariusz 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-149">Scenario 1.</span></span> <span data-ttu-id="06b32-150">Włącz rozszerzenie z domyślnego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="06b32-150">Enable the extension with the default data set</span></span>

<span data-ttu-id="06b32-151">W wersji 2.3 lub nowszej zawiera wartości domyślne, które będą zbierane:</span><span class="sxs-lookup"><span data-stu-id="06b32-151">In version 2.3 or later, the default data that will be collected includes:</span></span>

* <span data-ttu-id="06b32-152">Wszystkie informacje Rsyslog (w tym system, zabezpieczenia i dzienniki aplikacji).</span><span class="sxs-lookup"><span data-stu-id="06b32-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="06b32-153">Podstawowy zestaw danych systemowych podstawy.</span><span class="sxs-lookup"><span data-stu-id="06b32-153">A core set of basis system data.</span></span> <span data-ttu-id="06b32-154">Należy pamiętać, że pełny zestaw danych jest opisany w [lokacji rozwiązania Cross platformy w programie System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="06b32-154">Note that the full data set is described on the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="06b32-155">Jeśli chcesz włączyć dodatkowe dane, wykonaj czynności w scenariuszach 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="06b32-155">If you want to enable extra data, continue with the steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="06b32-156">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-156">Step 1.</span></span> <span data-ttu-id="06b32-157">Utwórz plik o nazwie PrivateConfig.json o następującej treści:</span><span class="sxs-lookup"><span data-stu-id="06b32-157">Create a file named PrivateConfig.json with the following content:</span></span>

    {
        "storageAccountName" : "the storage account to receive data",
        "storageAccountKey" : "the key of the account"
    }

<span data-ttu-id="06b32-158">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="06b32-158">Step 2.</span></span> <span data-ttu-id="06b32-159">Uruchom  **vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2 ustawić rozszerzenia maszyny wirtualnej platformy azure.* — PrivateConfig.json prywatnego config-path**.</span><span class="sxs-lookup"><span data-stu-id="06b32-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-the-performance-monitor-metrics"></a><span data-ttu-id="06b32-160">Scenariusz 2.</span><span class="sxs-lookup"><span data-stu-id="06b32-160">Scenario 2.</span></span> <span data-ttu-id="06b32-161">Dostosowanie metryk monitora wydajności</span><span class="sxs-lookup"><span data-stu-id="06b32-161">Customize the performance monitor metrics</span></span>

<span data-ttu-id="06b32-162">Ta sekcja opisuje sposób dostosowywania wydajności i tabelę danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="06b32-162">This section describes how to customize the performance and diagnostic data table.</span></span>

<span data-ttu-id="06b32-163">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-163">Step 1.</span></span> <span data-ttu-id="06b32-164">Utwórz plik o nazwie PrivateConfig.json z zawartością, który został opisany w scenariuszu 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-164">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="06b32-165">Utwórz również plik o nazwie PublicConfig.json.</span><span class="sxs-lookup"><span data-stu-id="06b32-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="06b32-166">Umożliwia określenie danych, które mają być zbierane.</span><span class="sxs-lookup"><span data-stu-id="06b32-166">Specify the particular data you want to collect.</span></span>

<span data-ttu-id="06b32-167">Dla wszystkich obsługiwanych dostawców i zmienne odwołania [lokacji rozwiązania Cross platformy w programie System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="06b32-167">For all supported providers and variables, reference the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="06b32-168">Możesz mieć wiele zapytań i przechowywać je w wielu tabel, dodając więcej kwerend do skryptu.</span><span class="sxs-lookup"><span data-stu-id="06b32-168">You can have multiple queries and store them in multiple tables by appending more queries to the script.</span></span>

<span data-ttu-id="06b32-169">Domyślnie dane Rsyslog zawsze są zbierane.</span><span class="sxs-lookup"><span data-stu-id="06b32-169">By default, the Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="06b32-170">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="06b32-170">Step 2.</span></span> <span data-ttu-id="06b32-171">Uruchom  **vm_name LinuxDiagnostic Microsoft.OSTCExtensions "2 ustawić rozszerzenia maszyny wirtualnej platformy azure.*"--prywatnego config-path PrivateConfig.json — PublicConfig.json publicznego config-path**.</span><span class="sxs-lookup"><span data-stu-id="06b32-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="06b32-172">Scenariusz 3.</span><span class="sxs-lookup"><span data-stu-id="06b32-172">Scenario 3.</span></span> <span data-ttu-id="06b32-173">Przekazanie plików dzienników</span><span class="sxs-lookup"><span data-stu-id="06b32-173">Upload your own log files</span></span>

<span data-ttu-id="06b32-174">W tej sekcji opisano, jak do gromadzenia i przekazywania określone pliki dziennika na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="06b32-174">This section describes how to collect and upload specific log files to your storage account.</span></span> <span data-ttu-id="06b32-175">Należy określić ścieżkę do pliku dziennika i nazwę tabeli, w której chcesz zapisać dziennik.</span><span class="sxs-lookup"><span data-stu-id="06b32-175">You need to specify both the path to your log file and the name of the table where you want to store your log.</span></span> <span data-ttu-id="06b32-176">Można utworzyć wiele plików dziennika, dodając wiele wpisów tabeli/plików do skryptu.</span><span class="sxs-lookup"><span data-stu-id="06b32-176">You can create multiple log files by adding multiple file/table entries to the script.</span></span>

<span data-ttu-id="06b32-177">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-177">Step 1.</span></span> <span data-ttu-id="06b32-178">Utwórz plik o nazwie PrivateConfig.json z zawartością, który został opisany w scenariuszu 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-178">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="06b32-179">Następnie utwórz plik o nazwie PublicConfig.json o następującej treści:</span><span class="sxs-lookup"><span data-stu-id="06b32-179">Then create another file named PublicConfig.json with the following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="06b32-180">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="06b32-180">Step 2.</span></span> <span data-ttu-id="06b32-181">Uruchom polecenie `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="06b32-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="06b32-182">Należy pamiętać, że to ustawienie w wersjach rozszerzenia przed 2.3 wszystkie dzienniki zapisane `/var/log/mysql.err` mogą być zduplikowane do `/var/log/syslog` (lub `/var/log/messages` w zależności od Linux distro) również.</span><span class="sxs-lookup"><span data-stu-id="06b32-182">Note that with this setting on the extension versions prior to 2.3, all logs written to `/var/log/mysql.err` might be duplicated to `/var/log/syslog` (or `/var/log/messages` depending on the Linux distro) as well.</span></span> <span data-ttu-id="06b32-183">Jeśli chcesz uniknąć zduplikowanych rejestrowanie, można wykluczyć rejestrowanie `local6` zakładzie dzienniki w konfiguracji rsyslog.</span><span class="sxs-lookup"><span data-stu-id="06b32-183">If you'd like to avoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="06b32-184">Zależy on od Linux distro, ale w systemie Ubuntu 14.04 jest plik, aby zmodyfikować `/etc/rsyslog.d/50-default.conf` można zastąpić wiersza `*.*;auth,authpriv.none -/var/log/syslog` do `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="06b32-184">It depends on the Linux distro, but on an Ubuntu 14.04 system, the file to modify is `/etc/rsyslog.d/50-default.conf` and you can replace the line `*.*;auth,authpriv.none -/var/log/syslog` to `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="06b32-185">Tego problemu w najnowszym wydaniu poprawki 2.3 (2.3.9007), więc jeśli wersja rozszerzenia 2.3, ten problem nie powinno się zdarzyć.</span><span class="sxs-lookup"><span data-stu-id="06b32-185">This issue is fixed in the latest hotfix release of 2.3 (2.3.9007), so if you have the extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="06b32-186">Jeśli nadal nie nawet po ponownym uruchomieniu maszyny Wirtualnej, skontaktuj się z nami i pomóc nam Rozwiązywanie problemów z powodu najnowszej wersji poprawki nie jest instalowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="06b32-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why the latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-the-extension-from-collecting-any-logs"></a><span data-ttu-id="06b32-187">Scenariusz 4.</span><span class="sxs-lookup"><span data-stu-id="06b32-187">Scenario 4.</span></span> <span data-ttu-id="06b32-188">Zatrzymaj rozszerzenia ze zbierania żadnych dzienników</span><span class="sxs-lookup"><span data-stu-id="06b32-188">Stop the extension from collecting any logs</span></span>

<span data-ttu-id="06b32-189">W tej sekcji opisano, jak zatrzymać rozszerzenia ze zbierania dzienników.</span><span class="sxs-lookup"><span data-stu-id="06b32-189">This section describes how to stop the extension from collecting logs.</span></span> <span data-ttu-id="06b32-190">Należy pamiętać, że proces agenta monitorowania będzie nadal uruchomione i działają prawidłowo nawet w przypadku tego procesu ponownej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="06b32-190">Note that the monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="06b32-191">Jeśli chcesz całkowicie zatrzymać procesu agenta monitorowania, możesz to zrobić po wyłączeniu rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="06b32-191">If you'd like to stop the monitoring agent process completely, you can do so by disabling the extension.</span></span> <span data-ttu-id="06b32-192">To polecenie, aby wyłączyć rozszerzenie `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="06b32-192">The command to disable the extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="06b32-193">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-193">Step 1.</span></span> <span data-ttu-id="06b32-194">Utwórz plik o nazwie PrivateConfig.json z zawartością, który został opisany w scenariuszu 1.</span><span class="sxs-lookup"><span data-stu-id="06b32-194">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="06b32-195">Utwórz plik o nazwie PublicConfig.json o następującej treści:</span><span class="sxs-lookup"><span data-stu-id="06b32-195">Create another file named PublicConfig.json with the following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="06b32-196">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="06b32-196">Step 2.</span></span> <span data-ttu-id="06b32-197">Uruchom  **vm_name LinuxDiagnostic Microsoft.OSTCExtensions "2 ustawić rozszerzenia maszyny wirtualnej platformy azure.*"--prywatnego config-path PrivateConfig.json — PublicConfig.json publicznego config-path**.</span><span class="sxs-lookup"><span data-stu-id="06b32-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="06b32-198">Przejrzyj dane</span><span class="sxs-lookup"><span data-stu-id="06b32-198">Review your data</span></span>

<span data-ttu-id="06b32-199">Wydajność i danych diagnostycznych są przechowywane w tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-199">The performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="06b32-200">Przegląd [jak używać magazynu tabel Azure w języku Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) więcej informacji na temat dostępu do danych w tabeli magazynu za pomocą skryptów wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06b32-200">Review [How to use Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) to learn how to access the data in the storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="06b32-201">Ponadto służy następujące narzędzia interfejsu użytkownika do uzyskania dostępu do danych:</span><span class="sxs-lookup"><span data-stu-id="06b32-201">In addition, you can use following UI tools to access the data:</span></span>

1. <span data-ttu-id="06b32-202">Eksplorator serwera programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06b32-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="06b32-203">Przejdź do swojego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="06b32-203">Go to your storage account.</span></span> <span data-ttu-id="06b32-204">Po uruchomieniu maszyny Wirtualnej dla około pięciu minut, zostanie wyświetlony w tabelach cztery domyślne: "LinuxCpu", "LinuxDisk", "LinuxMemory" i "Linuxsyslog".</span><span class="sxs-lookup"><span data-stu-id="06b32-204">After the VM runs for about five minutes, you'll see the four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="06b32-205">Kliknij dwukrotnie nazwy tabeli, aby wyświetlić dane.</span><span class="sxs-lookup"><span data-stu-id="06b32-205">Double-click the table names to view the data.</span></span>
1. <span data-ttu-id="06b32-206">[Eksplorator usługi Azure Storage](https://azurestorageexplorer.codeplex.com/ "Eksploratora usługi Azure Storage").</span><span class="sxs-lookup"><span data-stu-id="06b32-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![Obraz](./media/diagnostic-extension/no1.png)

<span data-ttu-id="06b32-208">Jeśli włączono fileCfg lub perfCfg (zgodnie z opisem w scenariuszach 2 i 3), można użyć programu Visual Studio w Eksploratorze serwera i Eksploratora usługi Storage platformy Azure do wyświetlania danych innych niż domyślne.</span><span class="sxs-lookup"><span data-stu-id="06b32-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer to view non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="06b32-209">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="06b32-209">Known issues</span></span>

* <span data-ttu-id="06b32-210">Rsyslog informacji i określić klienta pliku dziennika można uzyskać tylko za pomocą skryptów.</span><span class="sxs-lookup"><span data-stu-id="06b32-210">The Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
