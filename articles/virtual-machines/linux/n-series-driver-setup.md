---
title: "Instalacja sterownika N-series usługi Azure dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować wersji sterowników procesora GPU NVIDIA dla maszyn wirtualnych N-series systemem Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="874d8-103">Instalowanie sterowników NVIDIA GPU na maszynach wirtualnych N-series systemem Linux</span><span class="sxs-lookup"><span data-stu-id="874d8-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="874d8-104">Aby skorzystać z możliwości procesora GPU N-series maszyny wirtualne platformy Azure systemem Linux, zainstalować obsługiwanych NVIDIA grafiki sterowników.</span><span class="sxs-lookup"><span data-stu-id="874d8-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="874d8-105">Ten artykuł zawiera kroki konfiguracji sterownika po wdrożeniu maszyny Wirtualnej N serii.</span><span class="sxs-lookup"><span data-stu-id="874d8-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="874d8-106">Informacje o instalacji sterowników jest również dostępny do [maszyn wirtualnych systemu Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="874d8-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="874d8-107">Dane techniczne, wielkości magazynu i dysku szczegóły wirtualna N-series, zobacz [rozmiarów maszyn wirtualnych systemu Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="874d8-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="874d8-108">Zainstaluj sterowniki siatki dla maszyn wirtualnych z wirtualizacją sieci</span><span class="sxs-lookup"><span data-stu-id="874d8-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="874d8-109">Aby zainstalować sterowniki NVIDIA siatki na maszynach wirtualnych z wirtualizacją sieci, utworzyć połączenie SSH na każdej maszynie Wirtualnej i wykonaj procedurę dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="874d8-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="874d8-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="874d8-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="874d8-111">Uruchom `lspci` polecenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-111">Run the `lspci` command.</span></span> <span data-ttu-id="874d8-112">Sprawdź, czy karta NVIDIA M60 lub karty są widoczne jako PCI urządzenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="874d8-113">Zainstaluj aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="874d8-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="874d8-114">Wyłącz Nouveau sterownik jądra, który jest niezgodny ze sterownikiem NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="874d8-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="874d8-115">(Tylko użyć sterownika NVIDIA na maszynach wirtualnych z wirtualizacją sieci). W tym celu należy utworzyć plik w `/etc/modprobe.d `o nazwie `nouveau.conf` z następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="874d8-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="874d8-116">Ponowny rozruch maszyny Wirtualnej i ponownie.</span><span class="sxs-lookup"><span data-stu-id="874d8-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="874d8-117">Serwer X zakończenia:</span><span class="sxs-lookup"><span data-stu-id="874d8-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="874d8-118">Pobieranie i instalowanie sterownika siatki:</span><span class="sxs-lookup"><span data-stu-id="874d8-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="874d8-119">Gdy pojawi się monit Czy chcesz uruchomić narzędzie nvidia xconfig aktualizacji X pliku konfiguracji, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="874d8-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="874d8-120">Po zakończeniu instalacji, skopiuj /etc/nvidia/gridd.conf.template do nowego gridd.conf pliku w lokalizacji/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="874d8-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="874d8-121">Dodaj następujący kod do `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="874d8-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="874d8-122">Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="874d8-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="874d8-123">Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="874d8-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="874d8-124">Jądra i DKMS aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="874d8-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="874d8-125">Wyłącz Nouveau sterownik jądra, który jest niezgodny ze sterownikiem NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="874d8-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="874d8-126">(Tylko użyć sterownika NVIDIA na maszynach wirtualnych z wirtualizacją sieci). W tym celu należy utworzyć plik w `/etc/modprobe.d `o nazwie `nouveau.conf` z następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="874d8-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="874d8-127">Ponowny rozruch maszyny Wirtualnej, połącz się ponownie i zainstalować najnowszą wersję usług integracji systemu Linux dla funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="874d8-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="874d8-128">Ponowne łączenie się z maszyny Wirtualnej i uruchom `lspci` polecenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="874d8-129">Sprawdź, czy karta NVIDIA M60 lub karty są widoczne jako PCI urządzenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="874d8-130">Pobieranie i instalowanie sterownika siatki:</span><span class="sxs-lookup"><span data-stu-id="874d8-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="874d8-131">Gdy pojawi się monit Czy chcesz uruchomić narzędzie nvidia xconfig aktualizacji X pliku konfiguracji, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="874d8-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="874d8-132">Po zakończeniu instalacji, skopiuj /etc/nvidia/gridd.conf.template do nowego gridd.conf pliku w lokalizacji/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="874d8-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="874d8-133">Dodaj następujący kod do `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="874d8-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="874d8-134">Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="874d8-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="874d8-135">Sprawdzić, czy instalacja sterownika</span><span class="sxs-lookup"><span data-stu-id="874d8-135">Verify driver installation</span></span>


<span data-ttu-id="874d8-136">Się zapytanie o stan urządzenia procesora GPU, SSH maszyny Wirtualnej i uruchom [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="874d8-137">Zostaną wyświetlone dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="874d8-137">Output similar to the following appears:</span></span>

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="874d8-139">X11 serwera</span><span class="sxs-lookup"><span data-stu-id="874d8-139">X11 server</span></span>
<span data-ttu-id="874d8-140">Jeśli potrzebujesz X11 serwera dla połączenia zdalne z wirtualizacją sieci maszyny Wirtualnej, [x11vnc](http://www.karlrunge.com/x11vnc/) jest zalecana, ponieważ umożliwia przyspieszanie sprzętowe grafiki.</span><span class="sxs-lookup"><span data-stu-id="874d8-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="874d8-141">BusID urządzenia M60 należy dodać ręcznie do pliku xconfig (`etc/X11/xorg.conf` na Ubuntu 16.04 LTS, `/etc/X11/XF86config` CentOS 7.3 lub Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="874d8-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="874d8-142">Dodaj `"Device"` sekcji podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="874d8-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="874d8-143">Ponadto aktualizacji z `"Screen"` sekcji, aby korzystać z tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="874d8-144">BusID znajduje się przez uruchomienie</span><span class="sxs-lookup"><span data-stu-id="874d8-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="874d8-145">BusID można zmienić, gdy maszyny Wirtualnej pobiera przydzielić lub ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="874d8-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="874d8-146">W związku z tym warto użyć skryptu, aby zaktualizować BusID w X11 konfiguracji po ponownym uruchomieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="874d8-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="874d8-147">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="874d8-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="874d8-148">Ten plik może być wywoływany jako główny na rozruch, tworząc wpis dla niego w `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="874d8-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="874d8-149">Zainstaluj sterowniki CUDA NC maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="874d8-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="874d8-150">Poniżej przedstawiono kroki, aby zainstalować sterowniki NVIDIA na maszynach wirtualnych NC Linux z NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="874d8-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="874d8-151">Deweloperzy C i C++ może opcjonalnie zainstalować pełny zestaw narzędzi do tworzenia aplikacji przyspieszony procesora GPU.</span><span class="sxs-lookup"><span data-stu-id="874d8-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="874d8-152">Aby uzyskać więcej informacji, zobacz [Przewodnik instalacji CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="874d8-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="874d8-153">Łącza pobierania sterowników CUDA podane w tym miejscu są aktualne w momencie publikacji.</span><span class="sxs-lookup"><span data-stu-id="874d8-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="874d8-154">Najnowsze sterowniki CUDA, odwiedź stronę [NVIDIA](http://www.nvidia.com/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="874d8-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="874d8-155">Aby zainstalować zestaw narzędzi CUDA, należy utworzyć połączenie SSH na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="874d8-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="874d8-156">Aby zweryfikować, że system ma obsługą CUDA procesora GPU, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="874d8-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="874d8-157">Zostaną wyświetlone dane wyjściowe podobne do poniższego przykładu (pokazywanie karty NVIDIA tesla — K80):</span><span class="sxs-lookup"><span data-stu-id="874d8-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![dane wyjściowe polecenia lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="874d8-159">Następnie uruchom instalację polecenia specyficzne dla dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="874d8-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="874d8-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="874d8-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="874d8-161">Pobierz i zainstaluj sterowniki CUDA.</span><span class="sxs-lookup"><span data-stu-id="874d8-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="874d8-162">Instalacja może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="874d8-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="874d8-163">Opcjonalnie zainstalować pełny zestaw CUDA, wpisz:</span><span class="sxs-lookup"><span data-stu-id="874d8-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="874d8-164">Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="874d8-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="874d8-165">Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="874d8-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="874d8-166">Pobierz aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="874d8-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="874d8-167">Połącz się ponownie z maszyną wirtualną i zainstaluj najnowsze usługi integracji systemu Linux w funkcji Hyper-v.</span><span class="sxs-lookup"><span data-stu-id="874d8-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="874d8-168">Jeśli obraz na podstawie CentOS HPC jest zainstalowany na maszynie Wirtualnej NC24r, przejdź do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="874d8-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="874d8-169">Ponieważ sterowniki Azure RDMA i usługi integracji systemu Linux są wstępnie zainstalowane w obrazie, LIS nie powinny zostać uaktualnione, a aktualizacje jądra są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="874d8-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="874d8-170">Połącz się ponownie do maszyny Wirtualnej i kontynuować instalację za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="874d8-170">Reconnect to the VM and continue installation with the following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="874d8-171">Instalacja może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="874d8-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="874d8-172">Opcjonalnie zainstalować pełny zestaw CUDA, wpisz:</span><span class="sxs-lookup"><span data-stu-id="874d8-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="874d8-173">Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="874d8-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="874d8-174">Sprawdzić, czy instalacja sterownika</span><span class="sxs-lookup"><span data-stu-id="874d8-174">Verify driver installation</span></span>


<span data-ttu-id="874d8-175">Się zapytanie o stan urządzenia procesora GPU, SSH maszyny Wirtualnej i uruchom [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="874d8-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="874d8-176">Zostaną wyświetlone dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="874d8-176">Output similar to the following appears:</span></span>

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="874d8-178">Aktualizacje sterowników CUDA</span><span class="sxs-lookup"><span data-stu-id="874d8-178">CUDA driver updates</span></span>

<span data-ttu-id="874d8-179">Firma Microsoft zaleca okresowej aktualizacji sterowników CUDA po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="874d8-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="874d8-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="874d8-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="874d8-181">Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="874d8-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="874d8-182">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="874d8-182">Troubleshooting</span></span>

* <span data-ttu-id="874d8-183">Istnieje znany problem dotyczący CUDA sterowników w N-series maszyny wirtualne platformy Azure systemem jądra systemu Linux 4.4.0-75 Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="874d8-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="874d8-184">Jeśli uaktualniasz z wcześniejszej wersji jądra, uaktualnienie do co najmniej 4.4.0-77 wersji jądra.</span><span class="sxs-lookup"><span data-stu-id="874d8-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="874d8-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="874d8-185">Next steps</span></span>

* <span data-ttu-id="874d8-186">Aby uzyskać więcej informacji o NVIDIA GPU na maszynach wirtualnych N-series zobacz:</span><span class="sxs-lookup"><span data-stu-id="874d8-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="874d8-187">[NVIDIA tesla — K80](http://www.nvidia.com/object/tesla-k80.html) (w przypadku maszyn wirtualnych Azure NC)</span><span class="sxs-lookup"><span data-stu-id="874d8-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="874d8-188">[NVIDIA tesla — M60](http://www.nvidia.com/object/tesla-m60.html) (w przypadku maszyn wirtualnych z wirtualizacją sieci Azure)</span><span class="sxs-lookup"><span data-stu-id="874d8-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="874d8-189">Aby przechwycić obraz maszyny Wirtualnej systemu Linux z zainstalowanych sterowników NVIDIA, zobacz [generalize i przechwytywaniu maszyny wirtualnej systemu Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="874d8-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
