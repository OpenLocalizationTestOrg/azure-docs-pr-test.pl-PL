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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Konfigurowanie wersji sterowników procesora GPU dla maszyn wirtualnych N-series, system operacyjny Windows Server
tootake korzystać z funkcji GPU hello Azure N-serii maszyn wirtualnych z systemem Windows Server 2016 lub Windows Server 2012 R2, zainstaluj obsługiwane NVIDIA sterowniki grafiki. Ten artykuł zawiera kroki konfiguracji sterownika po wdrożeniu maszyny Wirtualnej N serii. Informacje o instalacji sterowników jest również dostępny do [maszyn wirtualnych systemu Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dla podstawowych specyfikacji, pojemności magazynu i dysku szczegółów, zobacz [rozmiarów maszyn wirtualnych systemu Windows GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Instalacja sterownika

1. Połączenia pulpitu zdalnego tooeach N-series maszyny Wirtualnej.

2. Pobierz, Wyodrębnij i zainstalować sterownik hello obsługiwane dla systemu operacyjnego Windows.

Na maszynach wirtualnych z wirtualizacją sieci Azure po instalacji sterowników jest wymagane ponowne uruchomienie komputera. Na maszynach wirtualnych NC ponowne uruchomienie nie jest wymagane.

## <a name="verify-driver-installation"></a>Sprawdzić, czy instalacja sterownika

Instalacja sterownika w Menedżerze urządzeń można sprawdzić. Witaj poniższy przykład przedstawia Konfiguracja zakończyła się pomyślnie hello K80 tesla — karty na maszynie Wirtualnej platformy Azure NC.

![Właściwości sterownika procesora GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

Witaj tooquery GPU stanu urządzenia, uruchom hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem hello narzędzie wiersza polecenia.

1. Otwórz wiersz polecenia i zmień toohello **C:\Program Files\NVIDIA Corporation\NVSMI** katalogu.

2. Uruchom **nvidia smi**. Jeśli jest zainstalowany sterownik hello zobaczysz toobelow podobne dane wyjściowe. Należy pamiętać, że **GPU Util** pokazuje **0%** o ile nie są obecnie uruchomione obciążenie procesora GPU na powitania maszyny Wirtualnej.

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>RDMA sieci dla maszyn wirtualnych NC24r

Połączenie sieciowe RDMA można włączyć dla NC24r maszyn wirtualnych wdrożonych w hello tego samego zestawu dostępności. Hello HpcVmDrivers rozszerzenia muszą zostać dodane tooinstall sieci sterowniki urządzeń systemu Windows łączność RDMA. tooadd hello wirtualna rozszerzenia tooan NC24r maszyny Wirtualnej, użyj [programu Azure PowerShell](/powershell/azure/overview) poleceń cmdlet dla usługi Azure Resource Manager.

> [!NOTE]
> Obecnie tylko systemu Windows Server 2012 R2 obsługuje sieciowych RDMA hello na maszynach wirtualnych NC24r.
> 

tooinstall hello najnowszej wersji 1.1 HpcVMDrivers rozszerzenia na istniejącej maszyny Wirtualnej z funkcją RDMA o nazwie myVM regionu zachodnie stany USA hello:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyny wirtualnej i funkcje systemu Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hello RDMA sieci obsługuje ruch interfejsu Message (Passing) dla aplikacji działających z [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) lub Intel MPI 5.x. 


## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji dotyczących hello NVIDIA GPU na powitania N serii maszyn wirtualnych zobacz:
    * [NVIDIA tesla — K80](http://www.nvidia.com/object/tesla-k80.html) (w przypadku maszyn wirtualnych Azure NC)
    * [NVIDIA tesla — M60](http://www.nvidia.com/object/tesla-m60.html) (w przypadku maszyn wirtualnych z wirtualizacją sieci Azure)

* Deweloperzy tworzący aplikacje przyspieszony GPU dla jednostki GPU tesla — NVIDIA hello można również pobrać i zainstalować hello CUDA Toolkit 8 dla [systemu Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) lub [systemu Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


