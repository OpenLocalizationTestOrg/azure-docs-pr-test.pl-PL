---
title: ustawienia sterownika aaaAzure N-series dla systemu Linux | Dokumentacja firmy Microsoft
description: "Jak tooset się wersji sterowników procesora GPU NVIDIA dla maszyn wirtualnych N-series systemem Linux na platformie Azure"
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
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="511e8-103">Instalowanie sterowników NVIDIA GPU na maszynach wirtualnych N-series systemem Linux</span><span class="sxs-lookup"><span data-stu-id="511e8-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="511e8-104">tootake korzystać z funkcji GPU hello Azure N-serii maszyn wirtualnych z systemem Linux, sterowniki grafiki NVIDIA obsługiwane instalacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="511e8-105">Ten artykuł zawiera kroki konfiguracji sterownika po wdrożeniu maszyny Wirtualnej N serii.</span><span class="sxs-lookup"><span data-stu-id="511e8-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="511e8-106">Informacje o instalacji sterowników jest również dostępny do [maszyn wirtualnych systemu Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="511e8-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="511e8-107">Dane techniczne, wielkości magazynu i dysku szczegóły wirtualna N-series, zobacz [rozmiarów maszyn wirtualnych systemu Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="511e8-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="511e8-108">Zainstaluj sterowniki siatki dla maszyn wirtualnych z wirtualizacją sieci</span><span class="sxs-lookup"><span data-stu-id="511e8-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="511e8-109">sterowniki siatki NVIDIA tooinstall na maszynach wirtualnych z wirtualizacją sieci, należy tooeach połączenia SSH maszyny Wirtualnej i wykonaj kroki hello dla dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="511e8-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="511e8-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="511e8-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="511e8-111">Uruchom hello `lspci` polecenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-111">Run hello `lspci` command.</span></span> <span data-ttu-id="511e8-112">Sprawdź, czy karta hello NVIDIA M60 lub karty są widoczne jako PCI urządzenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="511e8-113">Zainstaluj aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="511e8-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="511e8-114">Wyłącz hello Nouveau jądra sterownika, który jest niezgodny z hello NVIDIA sterownika.</span><span class="sxs-lookup"><span data-stu-id="511e8-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="511e8-115">(Tylko użyć sterownika NVIDIA hello na maszynach wirtualnych z wirtualizacją sieci). toodo, Utwórz plik w `/etc/modprobe.d `o nazwie `nouveau.conf` z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="511e8-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="511e8-116">Uruchom ponownie hello maszyny Wirtualnej, a następnie ponownie.</span><span class="sxs-lookup"><span data-stu-id="511e8-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="511e8-117">Serwer X zakończenia:</span><span class="sxs-lookup"><span data-stu-id="511e8-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="511e8-118">Pobieranie i instalowanie sterownika siatki hello:</span><span class="sxs-lookup"><span data-stu-id="511e8-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="511e8-119">Pytanie, czy ma toorun hello nvidia xconfig narzędzie tooupdate X pliku konfiguracji, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="511e8-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="511e8-120">Po zakończeniu instalacji, skopiuj /etc/nvidia/gridd.conf.template tooa nowego pliku gridd.conf w lokalizacji/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="511e8-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="511e8-121">Dodaje hello zbyt`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="511e8-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="511e8-122">Ponowny rozruch hello maszyny Wirtualnej i kontynuować tooverify hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="511e8-123">Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="511e8-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="511e8-124">Jądra hello i DKMS aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="511e8-125">Wyłącz hello Nouveau jądra sterownika, który jest niezgodny z hello NVIDIA sterownika.</span><span class="sxs-lookup"><span data-stu-id="511e8-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="511e8-126">(Tylko użyć sterownika NVIDIA hello na maszynach wirtualnych z wirtualizacją sieci). toodo, Utwórz plik w `/etc/modprobe.d `o nazwie `nouveau.conf` z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="511e8-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="511e8-127">Ponowny rozruch hello maszyny Wirtualnej, połącz się ponownie i zainstalować najnowszą wersję usług integracji systemu Linux dla funkcji Hyper-V: hello</span><span class="sxs-lookup"><span data-stu-id="511e8-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="511e8-128">Połącz się ponownie toohello maszyny Wirtualnej i uruchom hello `lspci` polecenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="511e8-129">Sprawdź, czy karta hello NVIDIA M60 lub karty są widoczne jako PCI urządzenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="511e8-130">Pobieranie i instalowanie sterownika siatki hello:</span><span class="sxs-lookup"><span data-stu-id="511e8-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="511e8-131">Pytanie, czy ma toorun hello nvidia xconfig narzędzie tooupdate X pliku konfiguracji, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="511e8-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="511e8-132">Po zakończeniu instalacji, skopiuj /etc/nvidia/gridd.conf.template tooa nowego pliku gridd.conf w lokalizacji/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="511e8-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="511e8-133">Dodaje hello zbyt`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="511e8-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="511e8-134">Ponowny rozruch hello maszyny Wirtualnej i kontynuować tooverify hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="511e8-135">Sprawdzić, czy instalacja sterownika</span><span class="sxs-lookup"><span data-stu-id="511e8-135">Verify driver installation</span></span>


<span data-ttu-id="511e8-136">tooquery hello stan urządzenia procesora GPU, SSH toohello maszyny Wirtualnej i wykonywania hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem hello narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="511e8-137">Zostaną wyświetlone dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="511e8-137">Output similar toohello following appears:</span></span>

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="511e8-139">X11 serwera</span><span class="sxs-lookup"><span data-stu-id="511e8-139">X11 server</span></span>
<span data-ttu-id="511e8-140">Jeśli potrzebujesz X11 serwera dla połączeń zdalnych tooan wirtualizacją sieci maszyny Wirtualnej, [x11vnc](http://www.karlrunge.com/x11vnc/) jest zalecana, ponieważ umożliwia przyspieszanie sprzętowe grafiki.</span><span class="sxs-lookup"><span data-stu-id="511e8-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="511e8-141">Hello BusID hello M60 urządzenia należy dodać ręcznie pliku xconfig toohello (`etc/X11/xorg.conf` na Ubuntu 16.04 LTS, `/etc/X11/XF86config` CentOS 7.3 lub Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="511e8-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="511e8-142">Dodaj `"Device"` sekcji podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="511e8-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="511e8-143">Ponadto aktualizacji z `"Screen"` sekcji toouse tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="511e8-144">Witaj BusID znajduje się przez uruchomienie</span><span class="sxs-lookup"><span data-stu-id="511e8-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="511e8-145">Witaj BusID można zmienić, gdy maszyny Wirtualnej pobiera przydzielić lub ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="511e8-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="511e8-146">W związku z tym można toouse hello tooupdate skryptu BusID w konfiguracji hello X11 po ponownym uruchomieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="511e8-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="511e8-147">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="511e8-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="511e8-148">Ten plik może być wywoływany jako główny na rozruch, tworząc wpis dla niego w `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="511e8-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="511e8-149">Zainstaluj sterowniki CUDA NC maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="511e8-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="511e8-150">Poniżej przedstawiono kroki tooinstall NVIDIA sterowników na maszynach wirtualnych NC Linux z hello NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="511e8-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="511e8-151">Deweloperzy C i C++ może opcjonalnie zainstalować hello pełne Toolkit toobuild przyspieszony GPU aplikacje.</span><span class="sxs-lookup"><span data-stu-id="511e8-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="511e8-152">Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="511e8-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="511e8-153">Łącza pobierania sterowników CUDA podane w tym miejscu są aktualne w momencie publikacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="511e8-154">Najnowsze sterowniki CUDA hello można znaleźć hello [NVIDIA](http://www.nvidia.com/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="511e8-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="511e8-155">tooinstall CUDA Toolkit należy tooeach połączenia SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="511e8-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="511e8-156">tooverify, który hello system ma obsługą CUDA procesora GPU, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="511e8-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="511e8-157">Zostaną wyświetlone dane wyjściowe toohello podobnie poniższy przykład (pokazywanie karty NVIDIA tesla — K80):</span><span class="sxs-lookup"><span data-stu-id="511e8-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![dane wyjściowe polecenia lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="511e8-159">Następnie uruchom instalację polecenia specyficzne dla dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="511e8-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="511e8-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="511e8-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="511e8-161">Pobierz i zainstaluj hello CUDA sterowniki.</span><span class="sxs-lookup"><span data-stu-id="511e8-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="511e8-162">Witaj, instalacja może trwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="511e8-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="511e8-163">toooptionally instalacji hello pełny CUDA zestaw, typ:</span><span class="sxs-lookup"><span data-stu-id="511e8-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="511e8-164">Ponowny rozruch hello maszyny Wirtualnej i kontynuować tooverify hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="511e8-165">Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="511e8-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="511e8-166">Pobierz aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="511e8-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="511e8-167">Połącz się ponownie toohello maszyny Wirtualnej i zainstaluj hello najnowsze usługi integracji systemu Linux dla funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="511e8-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="511e8-168">Po zainstalowaniu obrazu na podstawie CentOS HPC na maszynie Wirtualnej NC24r Pomiń tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="511e8-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="511e8-169">Ponieważ sterowniki Azure RDMA i usługi integracji systemu Linux są wstępnie zainstalowane w obrazie hello, LIS nie powinny zostać uaktualnione, a aktualizacje jądra są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="511e8-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="511e8-170">Połącz się ponownie toohello maszyny Wirtualnej i kontynuować instalację z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="511e8-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

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

  <span data-ttu-id="511e8-171">Witaj, instalacja może trwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="511e8-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="511e8-172">toooptionally instalacji hello pełny CUDA zestaw, typ:</span><span class="sxs-lookup"><span data-stu-id="511e8-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="511e8-173">Ponowny rozruch hello maszyny Wirtualnej i kontynuować tooverify hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="511e8-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="511e8-174">Sprawdzić, czy instalacja sterownika</span><span class="sxs-lookup"><span data-stu-id="511e8-174">Verify driver installation</span></span>


<span data-ttu-id="511e8-175">tooquery hello stan urządzenia procesora GPU, SSH toohello maszyny Wirtualnej i wykonywania hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem hello narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="511e8-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="511e8-176">Zostaną wyświetlone dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="511e8-176">Output similar toohello following appears:</span></span>

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="511e8-178">Aktualizacje sterowników CUDA</span><span class="sxs-lookup"><span data-stu-id="511e8-178">CUDA driver updates</span></span>

<span data-ttu-id="511e8-179">Firma Microsoft zaleca okresowej aktualizacji sterowników CUDA po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="511e8-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="511e8-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="511e8-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="511e8-181">Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="511e8-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="511e8-182">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="511e8-182">Troubleshooting</span></span>

* <span data-ttu-id="511e8-183">Istnieje znany problem dotyczący CUDA sterowników w N-series maszyny wirtualne platformy Azure systemem jądra systemu Linux 4.4.0-75 hello Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="511e8-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="511e8-184">Jeśli uaktualniasz z wcześniejszej wersji jądra, Uaktualnij tooat co najmniej 4.4.0-77 wersji jądra.</span><span class="sxs-lookup"><span data-stu-id="511e8-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="511e8-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="511e8-185">Next steps</span></span>

* <span data-ttu-id="511e8-186">Aby uzyskać więcej informacji dotyczących hello NVIDIA GPU na powitania N serii maszyn wirtualnych zobacz:</span><span class="sxs-lookup"><span data-stu-id="511e8-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="511e8-187">[NVIDIA tesla — K80](http://www.nvidia.com/object/tesla-k80.html) (w przypadku maszyn wirtualnych Azure NC)</span><span class="sxs-lookup"><span data-stu-id="511e8-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="511e8-188">[NVIDIA tesla — M60](http://www.nvidia.com/object/tesla-m60.html) (w przypadku maszyn wirtualnych z wirtualizacją sieci Azure)</span><span class="sxs-lookup"><span data-stu-id="511e8-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="511e8-189">toocapture obraz maszyny Wirtualnej systemu Linux z zainstalowanych sterowników NVIDIA, zobacz [jak toogeneralize i przechwycenia maszyny wirtualnej systemu Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="511e8-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
