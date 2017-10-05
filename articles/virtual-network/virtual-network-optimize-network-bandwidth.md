---
title: "Zoptymalizować przepływność sieci maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zoptymalizować przepływność sieci maszyny wirtualnej platformy Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="1f62c-103">Zoptymalizować przepływność sieci maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1f62c-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="1f62c-104">Maszyny wirtualne platformy Azure (VM) ma domyślne ustawienia sieci, które mogą być optymalizowane więcej przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="1f62c-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="1f62c-105">W tym artykule opisano, jak zoptymalizować przepływność sieci systemu Microsoft Azure Windows oraz maszyn wirtualnych systemu Linux, łącznie z głównych dystrybucje, takich jak Ubuntu i CentOS Red Hat.</span><span class="sxs-lookup"><span data-stu-id="1f62c-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="1f62c-106">Maszyna wirtualna z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="1f62c-106">Windows VM</span></span>

<span data-ttu-id="1f62c-107">Jeśli maszyna wirtualna systemu Windows jest obsługiwana z [przyspieszony sieci](virtual-network-create-vm-accelerated-networking.md), włączenie tej funkcji może być konfiguracją optymalną przepustowości.</span><span class="sxs-lookup"><span data-stu-id="1f62c-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="1f62c-108">Dla wszystkich innych maszyn wirtualnych systemu Windows przy użyciu skalowanie po stronie odbierającej (RSS) mogą skorzystać z wyższej przepustowości maksymalnej niż Maszynę wirtualną bez RSS.</span><span class="sxs-lookup"><span data-stu-id="1f62c-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="1f62c-109">Funkcja RSS mogą być wyłączone domyślnie na maszynie wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1f62c-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="1f62c-110">Wykonaj poniższe kroki, aby ustalić, czy włączono funkcję RSS i ją włączyć, jeśli jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="1f62c-110">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="1f62c-111">Wprowadź `Get-NetAdapterRss` polecenia programu PowerShell, aby zobaczyć, czy funkcja RSS jest włączone dla karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="1f62c-111">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="1f62c-112">W poniższym przykładzie danych wyjściowych zwrócony z `Get-NetAdapterRss`, funkcja RSS nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="1f62c-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="1f62c-113">Wprowadź następujące polecenie, aby włączyć funkcję RSS:</span><span class="sxs-lookup"><span data-stu-id="1f62c-113">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="1f62c-114">Poprzednie polecenie nie ma danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1f62c-114">The previous command does not have an output.</span></span> <span data-ttu-id="1f62c-115">Polecenie zmienić ustawienia karty Sieciowej, powodując utracie połączenia tymczasowego około jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="1f62c-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="1f62c-116">Okno dialogowe Reconnecting pojawia się podczas utraty połączenia.</span><span class="sxs-lookup"><span data-stu-id="1f62c-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="1f62c-117">Po próbie trzeci zwykle przywróceniu łączności.</span><span class="sxs-lookup"><span data-stu-id="1f62c-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="1f62c-118">Potwierdź, że funkcja RSS jest włączona na maszynie wirtualnej, wprowadzając `Get-NetAdapterRss` polecenie ponownie.</span><span class="sxs-lookup"><span data-stu-id="1f62c-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="1f62c-119">W przypadku powodzenia zwrócono następujący przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="1f62c-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="1f62c-120">Maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="1f62c-120">Linux VM</span></span>

<span data-ttu-id="1f62c-121">Funkcja RSS jest zawsze włączona domyślnie w maszynie Wirtualnej systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f62c-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="1f62c-122">Jądra systemu Linux wydane od stycznia 2017 r obejmują nowe opcje optymalizacji sieci, które umożliwiają maszyny Wirtualnej systemu Linux w celu osiągnięcia wyższej przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="1f62c-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="1f62c-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1f62c-123">Ubuntu</span></span>

<span data-ttu-id="1f62c-124">Aby uzyskać optymalizacji, najpierw zaktualizować najnowszą obsługiwaną wersję, począwszy od czerwca 2017, który jest:</span><span class="sxs-lookup"><span data-stu-id="1f62c-124">In order to get the optimization, first update to the latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="1f62c-125">Po ukończeniu aktualizacji, wprowadź następujące polecenia, aby pobrać najnowsze jądra:</span><span class="sxs-lookup"><span data-stu-id="1f62c-125">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="1f62c-126">Polecenie opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="1f62c-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="1f62c-127">Ubuntu Azure w wersji zapoznawczej jądra</span><span class="sxs-lookup"><span data-stu-id="1f62c-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="1f62c-128">Ten jądra systemu Linux Azure w wersji zapoznawczej nie może mieć taki sam poziom dostępności i niezawodności jako obrazy Marketplace i zwolnij jądra, które są zwykle dostępności.</span><span class="sxs-lookup"><span data-stu-id="1f62c-128">This Azure Linux Preview kernel may not have the same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="1f62c-129">Funkcja nie jest obsługiwane, mogą mieć ograniczone możliwości i nie może być tak niezawodna jak domyślnego jądra.</span><span class="sxs-lookup"><span data-stu-id="1f62c-129">The feature is not supported, may have constrained capabilities, and may not be as reliable as the default kernel.</span></span> <span data-ttu-id="1f62c-130">Nie należy używać tego jądra dla obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1f62c-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="1f62c-131">Instalując proponowanych jądra systemu Linux platformy Azure można osiągnąć znaczne przepustowość.</span><span class="sxs-lookup"><span data-stu-id="1f62c-131">Significant throughput performance can be achieved by installing the proposed Azure Linux kernel.</span></span> <span data-ttu-id="1f62c-132">Aby wypróbować ten jądra, Dodaj następujący wiersz do /etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="1f62c-132">To try this kernel, add this line to /etc/apt/sources.list</span></span>

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="1f62c-133">Następnie uruchom następujące polecenia, jako element główny.</span><span class="sxs-lookup"><span data-stu-id="1f62c-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="1f62c-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="1f62c-134">CentOS</span></span>

<span data-ttu-id="1f62c-135">Aby uzyskać optymalizacji, najpierw zaktualizować najnowszą obsługiwaną wersję, począwszy od 2017 lipca, który jest:</span><span class="sxs-lookup"><span data-stu-id="1f62c-135">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="1f62c-136">Po ukończeniu aktualizacji, należy zainstalować najnowsze usługi integracji systemu Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="1f62c-136">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="1f62c-137">LIS, zaczynając od 4.2.2-2 jest optymalizacji przepływności.</span><span class="sxs-lookup"><span data-stu-id="1f62c-137">The throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="1f62c-138">Wprowadź następujące polecenia, aby zainstalować usługi LIS:</span><span class="sxs-lookup"><span data-stu-id="1f62c-138">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="1f62c-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="1f62c-139">Red Hat</span></span>

<span data-ttu-id="1f62c-140">Aby uzyskać optymalizacji, najpierw zaktualizować najnowszą obsługiwaną wersję, począwszy od 2017 lipca, który jest:</span><span class="sxs-lookup"><span data-stu-id="1f62c-140">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="1f62c-141">Po ukończeniu aktualizacji, należy zainstalować najnowsze usługi integracji systemu Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="1f62c-141">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="1f62c-142">Optymalizacji przepływności jest LIS, zaczynając od 4.2.</span><span class="sxs-lookup"><span data-stu-id="1f62c-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="1f62c-143">Wprowadź następujące polecenia, aby pobrać i zainstalować LIS:</span><span class="sxs-lookup"><span data-stu-id="1f62c-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="1f62c-144">Dowiedz się więcej o Linux Integration Services wersji 4.2 dla funkcji Hyper-V przeglądając [stronę pobierania](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="1f62c-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f62c-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f62c-145">Next steps</span></span>
* <span data-ttu-id="1f62c-146">Teraz, gdy maszyna wirtualna jest optymalizowane, zobacz wynik z [przepustowości/przepływność, testowanie maszyny Wirtualnej Azure](virtual-network-bandwidth-testing.md) dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="1f62c-146">Now that the VM is optimized, see the result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="1f62c-147">Dowiedz się więcej o [sieci wirtualnej platformy Azure — często zadawane pytania (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="1f62c-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
