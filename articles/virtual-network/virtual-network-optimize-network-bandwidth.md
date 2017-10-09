---
title: "przepustowość sieci VM aaaOptimize | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toooptimize maszyny wirtualnej platformy Azure sieci przepływności."
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
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="9859d-103">Zoptymalizować przepływność sieci maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9859d-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="9859d-104">Maszyny wirtualne platformy Azure (VM) ma domyślne ustawienia sieci, które mogą być optymalizowane więcej przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="9859d-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="9859d-105">W tym artykule opisano, jak toooptimize sieci przepływności systemu Microsoft Azure Windows oraz maszyn wirtualnych systemu Linux, łącznie z głównych dystrybucje, takich jak Ubuntu i CentOS Red Hat.</span><span class="sxs-lookup"><span data-stu-id="9859d-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="9859d-106">Maszyna wirtualna z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="9859d-106">Windows VM</span></span>

<span data-ttu-id="9859d-107">Jeśli maszyna wirtualna systemu Windows jest obsługiwana z [przyspieszony sieci](virtual-network-create-vm-accelerated-networking.md), włączenie tej funkcji będzie hello optymalną konfigurację przepływności.</span><span class="sxs-lookup"><span data-stu-id="9859d-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="9859d-108">Dla wszystkich innych maszyn wirtualnych systemu Windows przy użyciu skalowanie po stronie odbierającej (RSS) mogą skorzystać z wyższej przepustowości maksymalnej niż Maszynę wirtualną bez RSS.</span><span class="sxs-lookup"><span data-stu-id="9859d-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="9859d-109">Funkcja RSS mogą być wyłączone domyślnie na maszynie wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="9859d-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="9859d-110">Zakończenie hello następujące kroki toodetermine, czy włączono funkcję RSS i tooenable go, jeśli jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="9859d-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="9859d-111">Wprowadź hello `Get-NetAdapterRss` toosee polecenia programu PowerShell, jeśli funkcja RSS jest włączone dla karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="9859d-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="9859d-112">W hello następujące przykładowe dane wyjściowe zwrócone z hello `Get-NetAdapterRss`, funkcja RSS nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="9859d-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="9859d-113">Wprowadź następujące polecenie tooenable RSS hello:</span><span class="sxs-lookup"><span data-stu-id="9859d-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="9859d-114">poprzednie polecenie Hello nie ma danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9859d-114">hello previous command does not have an output.</span></span> <span data-ttu-id="9859d-115">polecenie Hello zmienić ustawienia karty Sieciowej, powodując utracie połączenia tymczasowego około jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="9859d-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="9859d-116">Okno dialogowe Reconnecting pojawia się podczas hello utracie połączenia.</span><span class="sxs-lookup"><span data-stu-id="9859d-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="9859d-117">Po próbie trzeci hello zwykle przywróceniu łączności.</span><span class="sxs-lookup"><span data-stu-id="9859d-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="9859d-118">Upewnij się, że funkcja RSS jest włączone w hello maszyny Wirtualnej, wprowadzając hello `Get-NetAdapterRss` polecenie ponownie.</span><span class="sxs-lookup"><span data-stu-id="9859d-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="9859d-119">Jeśli to się powiedzie, jest zwracany hello następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9859d-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="9859d-120">Maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9859d-120">Linux VM</span></span>

<span data-ttu-id="9859d-121">Funkcja RSS jest zawsze włączona domyślnie w maszynie Wirtualnej systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9859d-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="9859d-122">Jądra systemu Linux wydane od stycznia 2017 r obejmują nowe opcje optymalizacji sieci, które umożliwiają wyższej przepustowości sieci maszyny Wirtualnej systemu Linux tooachieve.</span><span class="sxs-lookup"><span data-stu-id="9859d-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="9859d-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9859d-123">Ubuntu</span></span>

<span data-ttu-id="9859d-124">W kolejności tooget hello optymalizacji najpierw zaktualizować wersję toohello najnowsza wersja obsługiwana, począwszy od czerwca 2017, który jest:</span><span class="sxs-lookup"><span data-stu-id="9859d-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="9859d-125">Po ukończeniu aktualizacji hello wprowadź następujące polecenia tooget hello najnowsze jądra hello:</span><span class="sxs-lookup"><span data-stu-id="9859d-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="9859d-126">Polecenie opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="9859d-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="9859d-127">Ubuntu Azure w wersji zapoznawczej jądra</span><span class="sxs-lookup"><span data-stu-id="9859d-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="9859d-128">Ta wersja zapoznawcza Linux Azure jądra nie może mieć hello sam poziom dostępności i niezawodności jako obrazy Marketplace i jądra, które są zwykle wersji dostępności.</span><span class="sxs-lookup"><span data-stu-id="9859d-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="9859d-129">Funkcja Hello nie jest obsługiwane, mogą mieć ograniczone możliwości i nie może być tak niezawodna jak hello domyślnego jądra.</span><span class="sxs-lookup"><span data-stu-id="9859d-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="9859d-130">Nie należy używać tego jądra dla obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="9859d-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="9859d-131">Instalując hello proponowane jądra systemu Linux platformy Azure można osiągnąć znaczne przepustowość.</span><span class="sxs-lookup"><span data-stu-id="9859d-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="9859d-132">tootry to jądra, Dodaj ten too/etc/apt/sources.list wiersza</span><span class="sxs-lookup"><span data-stu-id="9859d-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="9859d-133">Następnie uruchom następujące polecenia, jako element główny.</span><span class="sxs-lookup"><span data-stu-id="9859d-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="9859d-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="9859d-134">CentOS</span></span>

<span data-ttu-id="9859d-135">W kolejności tooget hello optymalizacji najpierw zaktualizuj wersję toohello najnowsza wersja obsługiwana, począwszy od 2017 lipca, który jest:</span><span class="sxs-lookup"><span data-stu-id="9859d-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="9859d-136">Po ukończeniu aktualizacji hello instalacji hello usług najnowsze integracji systemu Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="9859d-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="9859d-137">optymalizacji przepływności Hello jest LIS, zaczynając od 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="9859d-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="9859d-138">Wprowadź następujące polecenia tooinstall LIS hello:</span><span class="sxs-lookup"><span data-stu-id="9859d-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="9859d-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="9859d-139">Red Hat</span></span>

<span data-ttu-id="9859d-140">W kolejności tooget hello optymalizacji najpierw zaktualizuj wersję toohello najnowsza wersja obsługiwana, począwszy od 2017 lipca, który jest:</span><span class="sxs-lookup"><span data-stu-id="9859d-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="9859d-141">Po ukończeniu aktualizacji hello instalacji hello usług najnowsze integracji systemu Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="9859d-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="9859d-142">optymalizacji przepływności Hello jest LIS, zaczynając od 4.2.</span><span class="sxs-lookup"><span data-stu-id="9859d-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="9859d-143">Wprowadź następujące polecenia toodownload hello i instalowania usług LIS:</span><span class="sxs-lookup"><span data-stu-id="9859d-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="9859d-144">Dowiedz się więcej o Linux Integration Services wersji 4.2 dla funkcji Hyper-V, wyświetlając hello [stronę pobierania](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="9859d-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9859d-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9859d-145">Next steps</span></span>
* <span data-ttu-id="9859d-146">Teraz, gdy hello maszyny Wirtualnej jest optymalizowane, zobacz wynik hello [przepustowości/przepływność, testowanie maszyny Wirtualnej Azure](virtual-network-bandwidth-testing.md) dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="9859d-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="9859d-147">Dowiedz się więcej o [sieci wirtualnej platformy Azure — często zadawane pytania (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="9859d-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
