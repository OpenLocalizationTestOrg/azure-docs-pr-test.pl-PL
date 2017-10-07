---
title: ustawienia sterownika aaaAzure N-series dla systemu Windows | Dokumentacja firmy Microsoft
description: "Jak tooset się wersji sterowników procesora GPU NVIDIA N serii maszyn wirtualnych systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="d6389-103">Konfigurowanie wersji sterowników procesora GPU dla maszyn wirtualnych N-series, system operacyjny Windows Server</span><span class="sxs-lookup"><span data-stu-id="d6389-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="d6389-104">tootake korzystać z funkcji GPU hello Azure N-serii maszyn wirtualnych z systemem Windows Server 2016 lub Windows Server 2012 R2, zainstaluj obsługiwane NVIDIA sterowniki grafiki.</span><span class="sxs-lookup"><span data-stu-id="d6389-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="d6389-105">Ten artykuł zawiera kroki konfiguracji sterownika po wdrożeniu maszyny Wirtualnej N serii.</span><span class="sxs-lookup"><span data-stu-id="d6389-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="d6389-106">Informacje o instalacji sterowników jest również dostępny do [maszyn wirtualnych systemu Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6389-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d6389-107">Dla podstawowych specyfikacji, pojemności magazynu i dysku szczegółów, zobacz [rozmiarów maszyn wirtualnych systemu Windows GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6389-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="d6389-108">Instalacja sterownika</span><span class="sxs-lookup"><span data-stu-id="d6389-108">Driver installation</span></span>

1. <span data-ttu-id="d6389-109">Połączenia pulpitu zdalnego tooeach N-series maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6389-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="d6389-110">Pobierz, Wyodrębnij i zainstalować sterownik hello obsługiwane dla systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="d6389-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="d6389-111">Na maszynach wirtualnych z wirtualizacją sieci Azure po instalacji sterowników jest wymagane ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="d6389-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="d6389-112">Na maszynach wirtualnych NC ponowne uruchomienie nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="d6389-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="d6389-113">Sprawdzić, czy instalacja sterownika</span><span class="sxs-lookup"><span data-stu-id="d6389-113">Verify driver installation</span></span>

<span data-ttu-id="d6389-114">Instalacja sterownika w Menedżerze urządzeń można sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="d6389-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="d6389-115">Witaj poniższy przykład przedstawia Konfiguracja zakończyła się pomyślnie hello K80 tesla — karty na maszynie Wirtualnej platformy Azure NC.</span><span class="sxs-lookup"><span data-stu-id="d6389-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Właściwości sterownika procesora GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="d6389-117">Witaj tooquery GPU stanu urządzenia, uruchom hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem hello narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d6389-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="d6389-118">Otwórz wiersz polecenia i zmień toohello **C:\Program Files\NVIDIA Corporation\NVSMI** katalogu.</span><span class="sxs-lookup"><span data-stu-id="d6389-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="d6389-119">Uruchom **nvidia smi**.</span><span class="sxs-lookup"><span data-stu-id="d6389-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="d6389-120">Jeśli jest zainstalowany sterownik hello zobaczysz toobelow podobne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d6389-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="d6389-121">Należy pamiętać, że **GPU Util** pokazuje **0%** o ile nie są obecnie uruchomione obciążenie procesora GPU na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6389-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="d6389-123">RDMA sieci dla maszyn wirtualnych NC24r</span><span class="sxs-lookup"><span data-stu-id="d6389-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="d6389-124">Połączenie sieciowe RDMA można włączyć dla NC24r maszyn wirtualnych wdrożonych w hello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="d6389-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="d6389-125">Hello HpcVmDrivers rozszerzenia muszą zostać dodane tooinstall sieci sterowniki urządzeń systemu Windows łączność RDMA.</span><span class="sxs-lookup"><span data-stu-id="d6389-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="d6389-126">tooadd hello wirtualna rozszerzenia tooan NC24r maszyny Wirtualnej, użyj [programu Azure PowerShell](/powershell/azure/overview) poleceń cmdlet dla usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6389-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="d6389-127">Obecnie tylko systemu Windows Server 2012 R2 obsługuje sieciowych RDMA hello na maszynach wirtualnych NC24r.</span><span class="sxs-lookup"><span data-stu-id="d6389-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="d6389-128">tooinstall hello najnowszej wersji 1.1 HpcVMDrivers rozszerzenia na istniejącej maszyny Wirtualnej z funkcją RDMA o nazwie myVM regionu zachodnie stany USA hello:</span><span class="sxs-lookup"><span data-stu-id="d6389-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="d6389-129">Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyny wirtualnej i funkcje systemu Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6389-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="d6389-130">Hello RDMA sieci obsługuje ruch interfejsu Message (Passing) dla aplikacji działających z [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) lub Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="d6389-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d6389-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6389-131">Next steps</span></span>

* <span data-ttu-id="d6389-132">Aby uzyskać więcej informacji dotyczących hello NVIDIA GPU na powitania N serii maszyn wirtualnych zobacz:</span><span class="sxs-lookup"><span data-stu-id="d6389-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="d6389-133">[NVIDIA tesla — K80](http://www.nvidia.com/object/tesla-k80.html) (w przypadku maszyn wirtualnych Azure NC)</span><span class="sxs-lookup"><span data-stu-id="d6389-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="d6389-134">[NVIDIA tesla — M60](http://www.nvidia.com/object/tesla-m60.html) (w przypadku maszyn wirtualnych z wirtualizacją sieci Azure)</span><span class="sxs-lookup"><span data-stu-id="d6389-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="d6389-135">Deweloperzy tworzący aplikacje przyspieszony GPU dla jednostki GPU tesla — NVIDIA hello można również pobrać i zainstalować hello CUDA Toolkit 8 dla [systemu Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) lub [systemu Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="d6389-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="d6389-136">Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="d6389-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


