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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>Instalowanie sterowników NVIDIA GPU na maszynach wirtualnych N-series systemem Linux

Aby skorzystać z możliwości procesora GPU N-series maszyny wirtualne platformy Azure systemem Linux, zainstalować obsługiwanych NVIDIA grafiki sterowników. Ten artykuł zawiera kroki konfiguracji sterownika po wdrożeniu maszyny Wirtualnej N serii. Informacje o instalacji sterowników jest również dostępny do [maszyn wirtualnych systemu Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


Dane techniczne, wielkości magazynu i dysku szczegóły wirtualna N-series, zobacz [rozmiarów maszyn wirtualnych systemu Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>Zainstaluj sterowniki siatki dla maszyn wirtualnych z wirtualizacją sieci

Aby zainstalować sterowniki NVIDIA siatki na maszynach wirtualnych z wirtualizacją sieci, utworzyć połączenie SSH na każdej maszynie Wirtualnej i wykonaj procedurę dystrybucji systemu Linux. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Uruchom `lspci` polecenia. Sprawdź, czy karta NVIDIA M60 lub karty są widoczne jako PCI urządzenia.

2. Zainstaluj aktualizacje.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Wyłącz Nouveau sterownik jądra, który jest niezgodny ze sterownikiem NVIDIA. (Tylko użyć sterownika NVIDIA na maszynach wirtualnych z wirtualizacją sieci). W tym celu należy utworzyć plik w `/etc/modprobe.d `o nazwie `nouveau.conf` z następującą zawartość:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Ponowny rozruch maszyny Wirtualnej i ponownie. Serwer X zakończenia:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Pobieranie i instalowanie sterownika siatki:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. Gdy pojawi się monit Czy chcesz uruchomić narzędzie nvidia xconfig aktualizacji X pliku konfiguracji, wybierz **tak**.

7. Po zakończeniu instalacji, skopiuj /etc/nvidia/gridd.conf.template do nowego gridd.conf pliku w lokalizacji/etc/nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Dodaj następujący kod do `/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3


1. Jądra i DKMS aktualizacji.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Wyłącz Nouveau sterownik jądra, który jest niezgodny ze sterownikiem NVIDIA. (Tylko użyć sterownika NVIDIA na maszynach wirtualnych z wirtualizacją sieci). W tym celu należy utworzyć plik w `/etc/modprobe.d `o nazwie `nouveau.conf` z następującą zawartość:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Ponowny rozruch maszyny Wirtualnej, połącz się ponownie i zainstalować najnowszą wersję usług integracji systemu Linux dla funkcji Hyper-V:
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Ponowne łączenie się z maszyny Wirtualnej i uruchom `lspci` polecenia. Sprawdź, czy karta NVIDIA M60 lub karty są widoczne jako PCI urządzenia.
 
5. Pobieranie i instalowanie sterownika siatki:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. Gdy pojawi się monit Czy chcesz uruchomić narzędzie nvidia xconfig aktualizacji X pliku konfiguracji, wybierz **tak**.

7. Po zakończeniu instalacji, skopiuj /etc/nvidia/gridd.conf.template do nowego gridd.conf pliku w lokalizacji/etc/nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Dodaj następujący kod do `/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.

### <a name="verify-driver-installation"></a>Sprawdzić, czy instalacja sterownika


Się zapytanie o stan urządzenia procesora GPU, SSH maszyny Wirtualnej i uruchom [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem narzędzie wiersza polecenia. 

Zostaną wyświetlone dane wyjściowe podobne do następujących:

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>X11 serwera
Jeśli potrzebujesz X11 serwera dla połączenia zdalne z wirtualizacją sieci maszyny Wirtualnej, [x11vnc](http://www.karlrunge.com/x11vnc/) jest zalecana, ponieważ umożliwia przyspieszanie sprzętowe grafiki. BusID urządzenia M60 należy dodać ręcznie do pliku xconfig (`etc/X11/xorg.conf` na Ubuntu 16.04 LTS, `/etc/X11/XF86config` CentOS 7.3 lub Red Hat Enterprise Server 7.3). Dodaj `"Device"` sekcji podobny do następującego:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Ponadto aktualizacji z `"Screen"` sekcji, aby korzystać z tego urządzenia.
 
BusID znajduje się przez uruchomienie

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
BusID można zmienić, gdy maszyny Wirtualnej pobiera przydzielić lub ponownego uruchomienia. W związku z tym warto użyć skryptu, aby zaktualizować BusID w X11 konfiguracji po ponownym uruchomieniu maszyny Wirtualnej. Na przykład:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Ten plik może być wywoływany jako główny na rozruch, tworząc wpis dla niego w `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>Zainstaluj sterowniki CUDA NC maszyn wirtualnych

Poniżej przedstawiono kroki, aby zainstalować sterowniki NVIDIA na maszynach wirtualnych NC Linux z NVIDIA CUDA Toolkit 8.0. 

Deweloperzy C i C++ może opcjonalnie zainstalować pełny zestaw narzędzi do tworzenia aplikacji przyspieszony procesora GPU. Aby uzyskać więcej informacji, zobacz [Przewodnik instalacji CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> Łącza pobierania sterowników CUDA podane w tym miejscu są aktualne w momencie publikacji. Najnowsze sterowniki CUDA, odwiedź stronę [NVIDIA](http://www.nvidia.com/) witryny sieci Web.
>

Aby zainstalować zestaw narzędzi CUDA, należy utworzyć połączenie SSH na każdej maszynie Wirtualnej. Aby zweryfikować, że system ma obsługą CUDA procesora GPU, uruchom następujące polecenie:

```bash
lspci | grep -i NVIDIA
```
Zostaną wyświetlone dane wyjściowe podobne do poniższego przykładu (pokazywanie karty NVIDIA tesla — K80):

![dane wyjściowe polecenia lspci](./media/n-series-driver-setup/lspci.png)

Następnie uruchom instalację polecenia specyficzne dla dystrybucji.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Pobierz i zainstaluj sterowniki CUDA.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  Instalacja może zająć kilka minut.

2. Opcjonalnie zainstalować pełny zestaw CUDA, wpisz:

  ```bash
  sudo apt-get install cuda
  ```

3. Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3

1. Pobierz aktualizacje. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Połącz się ponownie z maszyną wirtualną i zainstaluj najnowsze usługi integracji systemu Linux w funkcji Hyper-v.

  > [!IMPORTANT]
  > Jeśli obraz na podstawie CentOS HPC jest zainstalowany na maszynie Wirtualnej NC24r, przejdź do kroku 3. Ponieważ sterowniki Azure RDMA i usługi integracji systemu Linux są wstępnie zainstalowane w obrazie, LIS nie powinny zostać uaktualnione, a aktualizacje jądra są domyślnie wyłączone.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Połącz się ponownie do maszyny Wirtualnej i kontynuować instalację za pomocą następujących poleceń:

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

  Instalacja może zająć kilka minut. 

4. Opcjonalnie zainstalować pełny zestaw CUDA, wpisz:

  ```bash
  sudo yum install cuda
  ```

5. Ponowny rozruch maszyny Wirtualnej, a następnie przejdź do weryfikacji instalacji.


### <a name="verify-driver-installation"></a>Sprawdzić, czy instalacja sterownika


Się zapytanie o stan urządzenia procesora GPU, SSH maszyny Wirtualnej i uruchom [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) zainstalowane ze sterownikiem narzędzie wiersza polecenia. 

Zostaną wyświetlone dane wyjściowe podobne do następujących:

![Stan urządzenia NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>Aktualizacje sterowników CUDA

Firma Microsoft zaleca okresowej aktualizacji sterowników CUDA po wdrożeniu.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Na podstawie centOS 7.3 lub Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Rozwiązywanie problemów

* Istnieje znany problem dotyczący CUDA sterowników w N-series maszyny wirtualne platformy Azure systemem jądra systemu Linux 4.4.0-75 Ubuntu 16.04 LTS. Jeśli uaktualniasz z wcześniejszej wersji jądra, uaktualnienie do co najmniej 4.4.0-77 wersji jądra. 



## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji o NVIDIA GPU na maszynach wirtualnych N-series zobacz:
    * [NVIDIA tesla — K80](http://www.nvidia.com/object/tesla-k80.html) (w przypadku maszyn wirtualnych Azure NC)
    * [NVIDIA tesla — M60](http://www.nvidia.com/object/tesla-m60.html) (w przypadku maszyn wirtualnych z wirtualizacją sieci Azure)

* Aby przechwycić obraz maszyny Wirtualnej systemu Linux z zainstalowanych sterowników NVIDIA, zobacz [generalize i przechwytywaniu maszyny wirtualnej systemu Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
