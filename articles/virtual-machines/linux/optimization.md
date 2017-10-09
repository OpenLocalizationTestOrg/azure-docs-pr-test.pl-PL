---
title: aaaOptimize maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, niektóre wskazówki optymalizacji toomake się, że po skonfigurowaniu sieci maszyny Wirtualnej systemu Linux, aby uzyskać optymalną wydajność na platformie Azure"
keywords: maszyny wirtualnej systemu Linux, maszyny wirtualnej systemu linux, ubuntu maszyny wirtualnej
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Optymalizowanie maszyny wirtualnej systemu Linux na platformie Azure
Tworzenie maszyny wirtualnej systemu Linux (VM) jest łatwe toodo z wiersza polecenia hello lub hello portalu. Ten samouczek pokazuje, jak tooensure po skonfigurowaniu go toooptimize jej wydajności na platformie Microsoft Azure hello. W tym temacie korzysta z maszyny Wirtualnej systemu Ubuntu Server, ale można również utworzyć maszynę wirtualną systemu Linux przy użyciu [obrazów jako szablon](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Wymagania wstępne
W tym temacie założono, masz już działający subskrypcji platformy Azure ([zakładania wersji próbnej](https://azure.microsoft.com/pricing/free-trial/)) i ma już skonfigurowanymi przez Maszynę wirtualną do Twojej subskrypcji platformy Azure. Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane w tooyour subskrypcji platformy Azure z [logowania az](/cli/azure/#login) przed [tworzenie maszyny Wirtualnej](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Azure dysku systemu operacyjnego
Po utworzeniu maszyny Wirtualnej systemu Linux na platformie Azure ma dwa dyski skojarzonych z nim. **/ dev/sda** dysku systemu operacyjnego jest **/dev/sdb** jest tymczasowy dysku.  Nie używaj hello głównego dysku systemu operacyjnego (**/dev/sda**) dla wszystkich elementów, z wyjątkiem hello systemu operacyjnego, w jakiej jest zoptymalizowana pod kątem szybkiego czasu rozruchu maszyny Wirtualnej i nie zapewniają dobrą wydajność dla obciążeń. Ma tooattach jeden lub więcej dysków tooyour wirtualna tooget trwałe i zoptymalizowane magazynu danych. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Dodawanie dysków dla rozmiaru i wydajności
Oparte na powitania rozmiar maszyny Wirtualnej, można dołączyć dodatkowe dyski too16 na A-Series, 32 dysków na D-Series i 64 dyski na komputerze serii G - każdego się too1 TB, rozmiar. Możesz dodać dodatkowe dyski w razie potrzeby na obszarze i wymagania IOps. Każdy dysk ma element docelowy wydajności 500 iops Standard Storage oraz IOps too5000 na dysku dla usługi Premium Storage.  Aby uzyskać więcej informacji dotyczących dysków Premium Storage, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla maszyn wirtualnych platformy Azure](../../storage/common/storage-premium-storage.md)

tooachieve hello najwyższy IOps na dyskach magazyn w warstwie Premium, gdy ich ustawień pamięci podręcznej ustawiono tooeither **tylko do odczytu** lub **Brak**, należy wyłączyć **bariery** podczas Instalowanie hello w systemie Linux. Nie ma potrzeby bariery, ponieważ hello zapisuje tooPremium magazynu kopii zapasowej dyski są trwałe dla tych ustawień pamięci podręcznej.

* Jeśli używasz **reiserFS**, wyłącz bariery przy użyciu opcji instalacji hello `barrier=none` (Włączanie bariery, użyj `barrier=flush`)
* Jeśli używasz **ext3/ext4**, wyłącz bariery przy użyciu opcji instalacji hello `barrier=0` (Włączanie bariery, użyj `barrier=1`)
* Jeśli używasz **XFS**, wyłącz bariery przy użyciu opcji instalacji hello `nobarrier` (umożliwiających bariery, użyj opcji hello `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Uwagi dotyczące konta magazynu niezarządzanego
Akcja domyślna Hello podczas tworzenia maszyny Wirtualnej z hello Azure CLI 2.0 jest toouse Azure zarządzanych dysków.  Te dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je.  Niezarządzane dyski wymagają konta magazynu i mają pewne zagadnienia dotyczące wydajności dodatkowe.  Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md).  Witaj w tej części opisano zagadnienia dotyczące wydajności tylko wtedy, gdy niezarządzany dysków.  Witaj ponownie, domyślna i toouse zarządzane dysków jest zalecane pamięci masowej.

Jeśli tworzysz Maszynę wirtualną z dyskami niezarządzane, upewnij się, dołączyć dyski z kont magazynu znajdującej się w hello sam region jako tooensure Twojego wirtualna bliskim sąsiedztwie i zminimalizować opóźnienie sieci.  Każde konto magazynu w warstwie standardowa może zawierać maksymalnie 20 k IOps i pojemności rozmiar 500 TB.  Ten limit działa się jednocześnie na dyskach hello systemu operacyjnego i wszelkie dyski danych utworzone w tym dyski tooapproximately 40 intensywnie używany. Dla kont Premium magazynu nie ma żadnego limitu maksymalna liczba IOps, ale ma limitu rozmiaru 32 TB. 

Gdy zajmowanie dużego obciążenia IOps i wybrano Standard Storage dla dysków, może być konieczne toosplit hello dysków między wieloma toomake kont magazynu się, że nie osiągnięto hello limit 20 000 IOps dla kont magazynu w warstwie standardowa. Maszyna wirtualna może zawierać kombinację dysków z różnych kont magazynu i tooachieve typy kont magazynu optymalną konfigurację.
 

## <a name="your-vm-temporary-drive"></a>Dysk tymczasowej maszyny Wirtualnej
Domyślnie podczas tworzenia maszyny Wirtualnej Azure zapewnia dysk systemu operacyjnego (**/dev/sda**) i dysku tymczasowym (**/dev/sdb**).  Wszystkie dyski dodatkowe dodać Pokaż się jako **/dev/sdc**, **/dev/sdd**, **/dev/które integrują usługi** i tak dalej. Wszystkie dane na dysku tymczasowego (**/dev/sdb**) nie są trwałe i mogą zostać utracone, jeśli określonych zdarzeń, takich jak rozmiar maszyny Wirtualnej, ponownego wdrażania, lub konserwacji wymusza ponowne uruchomienie maszyny wirtualnej.  Hello rozmiar i typ dysku tymczasowy jest powiązane toohello rozmiar maszyny Wirtualnej, wybrana w czasie wdrażania. Wszystkie hello premium rozmiar maszyn wirtualnych (seria DS, G i DS_V2) hello tymczasowej stacji obsługiwanych przez lokalny dysk SSD dodatkowe wydajności się too48k IOps. 

## <a name="linux-swap-file"></a>Plik wymiany systemu Linux
W przypadku maszyny Wirtualnej Azure z obrazu Ubuntu lub CoreOS, można użyć toosend CustomData inicjowaniem toocloud konfiguracji chmury. Jeśli użytkownik [przekazać obraz niestandardowy Linux](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) używającą chmury init, można także skonfigurować partycje wymiany przy użyciu chmury init.

Na obrazach chmury Ubuntu należy użyć init chmury tooconfigure hello wymiany partycji. Aby uzyskać więcej informacji, zobacz [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Obrazów nie obsługują chmury init wdrożone z hello Azure Marketplace obrazów maszyn wirtualnych ma zintegrowany z hello systemu operacyjnego agenta systemu Linux maszyny Wirtualnej. Ten agent umożliwia hello toointeract maszyny Wirtualnej z różnymi usługami platformy Azure. Zakładając, że wdrożono standardowy obraz z hello Azure Marketplace, będzie potrzebny toodo powitania po toocorrectly skonfigurować ustawienia pliku wymiany Linux:

Zlokalizuj i zmodyfikować dwóch wpisów w hello **/etc/waagent.conf** pliku. Decydować hello istnienie pliku wymiany dedykowanych i rozmiar pliku wymiany hello. Parametry Hello szukasz toomodify są `ResourceDisk.EnableSwap=N` i`ResourceDisk.SwapSizeMB=0` 

Zmień toohello parametry hello następujące ustawienia:

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size w MB toomeet potrzeb} 

Po dokonaniu zmiany hello muszą agenta waagent hello toorestart lub uruchom ponownie tooreflect Twojej maszyny Wirtualnej systemu Linux tych zmian.  Znasz hello zmiany zostały wprowadzone i utworzono pliku wymiany, gdy używasz hello `free` polecenia tooview wolnego miejsca. Witaj poniższym przykładzie przedstawiono plik wymiany 512MB utworzone w wyniku modyfikowanie hello **waagent.conf** pliku:

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>We/Wy planowania algorytm magazyn w warstwie Premium
Z hello 2.6.18 jądra systemu Linux we/wy hello domyślny algorytm planowania został zmieniony z tooCFQ ostateczny termin (całkowicie odpowiedniego algorytmu kolejkowania). W przypadku wzorców we/wy dostępie swobodnym istnieje niewielka różnica w wydajności różnice między CFQ a ostatecznym terminem.  W przypadku dysków na dyskach SSD, gdzie wzorca operacji We/Wy dysku hello jest głównie sekwencyjnych, przełączanie algorytmu toohello operacja lub ostatecznego terminu lepszą wydajność można uzyskać we/wy.

### <a name="view-hello-current-io-scheduler"></a>Widok hello bieżącego harmonogramu we/wy
Witaj Użyj następującego polecenia:  

```bash
cat /sys/block/sda/queue/scheduler
```

Możesz sprawdzić następujące dane wyjściowe, co oznacza hello bieżącego harmonogramu.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Zmień hello bieżącego urządzenia (/ dev/sda) operacji We/Wy planowania algorytmu
Witaj Użyj następującego polecenia:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> Zastosowanie tego ustawienia dla **/dev/sda** samodzielnie nie jest użyteczne. Ustaw na wszystkich dyskach danych, gdzie sekwencyjnych operacji We/Wy dominuje hello wzorca operacji We/Wy.  

Powinny pojawić się hello następujące dane wyjściowe, co oznacza, że **grub.cfg** pomyślnie odbudowany tego hello domyślny harmonogram został zaktualizowany tooNOOP.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Dla hello Redhat dystrybucji rodziny wystarczy hello następujące polecenie:   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>Przy użyciu nowszej tooachieve RAID oprogramowania I / Ops
Obciążeń wymagają IOps więcej niż jednego dysku, należy najpierw toouse konfiguracji RAID oprogramowania z wielu dysków. Ponieważ Azure wykonuje już odporności dysków w warstwie lokalnej sieci szkieletowej hello, możesz osiągnąć hello najwyższy poziom wydajności z konfiguracji RAID-0 rozkładanie.  Udostępnić i utworzyć dyski w hello środowiska platformy Azure i Dołącz do ich tooyour maszyny Wirtualnej systemu Linux przed partycjonowanie, formatowania i instalowanie hello dysków.  Więcej informacji na temat konfigurowania ustawień RAID oprogramowania na maszynie Wirtualnej systemu Linux na platformie azure można znaleźć w hello  **[Konfigurowanie RAID oprogramowania w systemie Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  dokumentu.

## <a name="next-steps"></a>Następne kroki
Pamiętaj, że z wszystkich dyskusji optymalizacji, testy tooperform przed i po każdej zmiany toomeasure hello wpływ hello zmiany ma.  Optymalizacja jest proces krok po kroku, który ma różne wyniki na różnych komputerach w danym środowisku.  Co działa w przypadku jednej konfiguracji mogą nie działać w innym osobom.

Niektóre zasoby tooadditional przydatne łącza: 

* [Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](../../storage/common/storage-premium-storage.md)
* [Podręcznik użytkownika Azure agenta systemu Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Optymalizacja wydajności MySQL na maszynach wirtualnych systemu Linux platformy Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Należy skonfigurować oprogramowanie RAID w systemie Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

