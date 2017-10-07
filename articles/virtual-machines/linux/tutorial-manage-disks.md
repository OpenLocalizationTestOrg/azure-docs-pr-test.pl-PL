---
title: dyski aaaManage Azure z hello Azure CLI | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie dyskami Azure z hello wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Zarządzanie dyskami Azure z hello wiersza polecenia platformy Azure

Maszyny wirtualne platformy Azure, użyj systemu operacyjnego dyski toostore hello maszyn wirtualnych, aplikacji i danych. Podczas tworzenia maszyny Wirtualnej jest ważne toochoose rozmiar dysku i obciążenia odpowiednie toohello oczekiwano konfiguracji. W tym samouczku opisano wdrażanie i Zarządzanie dyskami maszyny Wirtualnej. Informacje o:

> [!div class="checklist"]
> * Dyski systemu operacyjnego i tymczasowego
> * Dyski danych
> * Standard i dysków w warstwie Premium
> * Wydajność dysku
> * Dołączanie i przygotowywania dysków z danymi
> * Zmiana rozmiaru dysków
> * Migawki dysków


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Domyślna dysku systemu Azure

Po utworzeniu maszyny wirtualnej platformy Azure, dwa dyski są automatycznie dołączone toohello maszyny wirtualnej. 

**Dysk systemu operacyjnego** — dysków systemu operacyjnego mogą być określane w górę terabajt too1 i hosty hello maszyn wirtualnych systemu operacyjnego. ma oznaczenie dysku systemu operacyjnego Hello */dev/sda* domyślnie. Witaj dyskowej pamięci podręcznej konfiguracji dysku systemu operacyjnego hello jest zoptymalizowana pod kątem wydajności systemu operacyjnego. Z powodu tej konfiguracji hello dysk systemu operacyjnego **nie powinien** hosta aplikacji i danych. Dla aplikacji i danych użycia dysków danych, które opisano szczegółowo w dalszej części tego artykułu. 

**Dysku tymczasowym** -tymczasowego dysków używać dysków SSD, który znajduje się na powitania tego samego hosta platformy Azure jako hello maszyny Wirtualnej. Tymczasowy dyski są wysokiej wydajności i mogą być używane do operacji, takich jak przetwarzanie danych tymczasowych. Jednak hello maszyny Wirtualnej w przypadku tooa przeniesiony na nowy host, zostaną usunięte wszystkie dane przechowywane na dysku tymczasowym. rozmiar dysku tymczasowym hello Hello jest określana przez hello rozmiar maszyny Wirtualnej. Tymczasowe dyski są oznaczone jako */dev/sdb* i mieć punktu instalacji z *katalogu/mnt*.

### <a name="temporary-disk-sizes"></a>Rozmiary dysku tymczasowym

| Typ | Rozmiar maszyny Wirtualnej | Maksymalny rozmiar dysku tymczasowego (GB) |
|----|----|----|
| [Zastosowania ogólne](sizes-general.md) | A i serii D | 800 |
| [Optymalizacja pod kątem obliczeń](sizes-compute.md) | Seria F | 800 |
| [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md) | D i G serii | 6144 |
| [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md) | Seria L | 5630 |
| [Procesor GPU](sizes-gpu.md) | N serii | 1440 |
| [Wysoka wydajność](sizes-hpc.md) | A i serii H | 2000 |

## <a name="azure-data-disks"></a>Dyski danych Azure

Instalowanie aplikacji i przechowywania danych można dodać dodatkowego dysku z danymi. Dyski danych używanego w sytuacji, gdy wymagane jest trwałe i szybko reagowały pamięci masowej. Każdy dysk danych ma maksymalną pojemność 1 terabajt. rozmiar Hello hello maszyny wirtualnej Określa, jak wiele dysków z danymi mogą być dołączone tooa maszyny Wirtualnej. Dla każdej podstawowej maszyny Wirtualnej można dołączyć danych dwóch dysków. 

### <a name="max-data-disks-per-vm"></a>Maksymalna liczba dysków z danymi dla maszyny Wirtualnej

| Typ | Rozmiar maszyny Wirtualnej | Maksymalna liczba dysków z danymi dla maszyny Wirtualnej |
|----|----|----|
| [Zastosowania ogólne](sizes-general.md) | A i serii D | 32 |
| [Optymalizacja pod kątem obliczeń](sizes-compute.md) | Seria F | 32 |
| [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md) | D i G serii | 64 |
| [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md) | Seria L | 64 |
| [Procesor GPU](sizes-gpu.md) | N serii | 48 |
| [Wysoka wydajność](sizes-hpc.md) | A i serii H | 32 |

## <a name="vm-disk-types"></a>Typy dysków maszyny Wirtualnej

Platforma Azure oferuje dwa rodzaje dysku.

### <a name="standard-disk"></a>Dysków w warstwie standardowa

Magazyn Standard Storage bazuje na dyskach twardych (HDD) i stanowi ekonomiczne, chociaż wciąż wydajne rozwiązanie. Dyski standardowe idealnie nadają się do deweloperów ekonomiczne i testów obciążenia.

### <a name="premium-disk"></a>Dysku Premium

Dyski Premium bazują na dysk SSD dysku wysokiej wydajności i małych opóźnień. Idealny dla maszyn wirtualnych obciążeniu produkcji. Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-series i FS serii maszyn wirtualnych. Dysków w warstwie Premium są dostępne w trzech typów (P10, P20, P30), rozmiar hello dysku hello Określa typ dysku hello. Podczas wybierania, wartość hello rozmiaru dysku jest zaokrąglana toohello dalej typu. Na przykład jeśli rozmiar dysku hello jest mniejsza niż 128 GB, typ dysku hello jest P10. Jeśli rozmiar dysku hello wynosi 129 GB i 512, rozmiar hello jest P20. Niczego ponad 512 GB, rozmiar hello jest P30.

### <a name="premium-disk-performance"></a>Wydajność dysku Premium

|Typ dysku magazynu w warstwie Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Rozmiar dysku (zaokrąglony) | 128 GB | 512 GB | 1024 GB (1 TB) |
| Maksymalna liczba operacji wejścia/wyjścia na sekundę na dysk | 500 | 2,300 | 5,000 |
Przepływność na dysk | 100 MB/s | 150 MB/s | 200 MB/s |

Gdy hello powyżej tabeli określa maksymalną liczbę IOPS dla każdego dysku, można osiągnąć wyższy poziom wydajności przez stosowanie wielu dysków z danymi. Na przykład Standard_GS5 maszyny Wirtualnej można osiągnąć maksymalnie 80 000 IOPS. Aby uzyskać szczegółowe informacje o maksymalnej IOPS dla maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych systemu Linux](sizes.md).

## <a name="create-and-attach-disks"></a>Utwórz i Dołącz dysków

Dyski danych można tworzyć i dołączone w czasie tworzenia maszyny Wirtualnej lub tooan istniejącej maszyny Wirtualnej.

### <a name="attach-disk-at-vm-creation"></a>Dołączenie dysku podczas tworzenia maszyny Wirtualnej

Utwórz grupę zasobów o hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Utwórz maszynę Wirtualną przy użyciu hello [tworzenia maszyny wirtualnej az]( /cli/azure/vm#create) polecenia. Witaj `--datadisk-sizes-gb` argument jest używany toospecify, że dodatkowy dysk należy utworzyć i dołączyć toohello maszyny wirtualnej. toocreate i dołączyć więcej niż jeden dysk, użyj rozdzieloną spacjami listę wartości rozmiaru dysku. W hello poniższy przykład maszyna wirtualna zostanie utworzona z dwóch dysków, zarówno 128 GB. Ponieważ hello rozmiary dysków wynoszą 128 GB, te dyski obydwa są skonfigurowane jako P10s, które zapewniają maksymalną 500 IOPS dla każdego dysku.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Dołącz tooexisting dysku maszyny Wirtualnej

toocreate i dołączyć nowego dysku tooan istniejącej maszyny wirtualnej, użyj hello [dołączyć dysku maszyny wirtualnej az](/cli/azure/vm/disk#attach) polecenia. Witaj poniższy przykład tworzy dysk premium 128 GB w rozmiarze i dołącza go toohello maszyny Wirtualnej utworzone w ostatnim kroku hello.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Przygotowanie dysków z danymi

Po dysku maszyny wirtualnej podłączone toohello, system operacyjny hello musi toobe skonfigurowane toouse hello dysku. Witaj poniższy przykład pokazuje, jak toomanually konfigurowania dysku. Ten proces można również zautomatyzować, używając inicjowaniem chmury, które są objęte w [nowsze samouczek](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Konfiguracja ręczna

Utwórz połączenie SSH z maszyną wirtualną hello. Zastąp hello publicznego adresu IP maszyny wirtualnej hello hello przykładowego adresu IP.

```azurecli-interactive 
ssh 52.174.34.95
```

Witaj partycji z `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Zapis systemu plików toohello partycji przy użyciu hello `mkfs` polecenia.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Zainstaluj nowy dysk hello tak, aby była dostępna w systemie operacyjnym hello.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

dysk Hello jest teraz dostępna za pośrednictwem hello *datadrive* punktu instalacji, który można zweryfikować, uruchamiając hello `df -h` polecenia. 

```bash
df -h
```

dane wyjściowe Hello zawierają hello nowy dysk zainstalowany na */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure, który hello dysku jest ponownej instalacji po ponownym uruchomieniu, należy dodać go toohello */etc/fstab* pliku. toodo tak, Pobierz hello UUID dysku hello z hello `blkid` narzędzia.

```bash
sudo -i blkid
```

dane wyjściowe Hello Wyświetla hello identyfikatora UUID dysku hello `/dev/sdc1` w takim przypadku.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Dodaj wiersz toohello podobne, po toohello */etc/fstab* pliku. Również należy pamiętać, że zapis bariery można wyłączyć za pomocą *bariery = 0*, ta konfiguracja może poprawić wydajność dysku. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Teraz, gdy hello dysk został skonfigurowany, Zamknij sesję SSH hello.

```bash
exit
```

## <a name="resize-vm-disk"></a>Zmiana rozmiaru dysku maszyny Wirtualnej

Po wdrożeniu maszyny Wirtualnej, dysk systemu operacyjnego hello lub żadnych dysków dołączonych danych można zwiększyć rozmiar. Zwiększenie rozmiaru dysku hello jest korzystne w przypadku, gdy wymagające więcej miejsca do magazynowania lub wyższego poziomu wydajności (P10 P20, P30). Zauważ, że dyski nie można zmniejszyć rozmiar.

Przed zwiększeniem rozmiaru dysku, hello identyfikatora lub nazwy dysku hello jest wymagana. Użyj hello [Lista dysków az](/cli/azure/vm/disk#list) tooreturn polecenia wszystkich dysków w grupie zasobów. Zanotuj nazwę dysku hello chcesz tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

należy również deallocated Hello maszyny Wirtualnej. Użyj hello [deallocate wirtualna az]( /cli/azure/vm#deallocate) polecenia toostop i cofnięcia przydzielenia hello maszyny Wirtualnej.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Użyj hello [aktualizacja dysku az](/cli/azure/vm/disk#update) polecenia tooresize hello dysku. W tym przykładzie zmienia rozmiar dysku o nazwie *myDataDisk* too1 terabajt.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Po zakończeniu operacji zmiany rozmiaru hello start hello maszyny Wirtualnej.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Jeśli został zmieniony hello dysk systemu operacyjnego, jest automatycznie rozszerzana hello partycji. Jeśli zmieniono dysk z danymi, wszystkie partycje bieżącego muszą toobe rozwinięty w systemie operacyjnym hello maszyn wirtualnych.

## <a name="snapshot-azure-disks"></a>Migawki dysków Azure

Tworzenie migawki dysku tworzy odczytu tylko, w momencie kopię hello dysku. Migawki maszyny Wirtualnej platformy Azure są przydatne do szybkiego Zapisywanie stanu hello maszyny wirtualnej przed wprowadzeniem zmian w konfiguracji. W przypadku hello hello zmian konfiguracji potwierdzenia toobe niepożądane, można przywrócić stan maszyny Wirtualnej przy użyciu hello migawki. Gdy maszyna wirtualna ma więcej niż jeden dysk, migawki każdego dysku, niezależnie od hello innych użytkowników. Do wykonywania kopii zapasowych spójności aplikacji, należy wziąć pod uwagę zatrzymywanie hello maszyny Wirtualnej przed wykonaniem migawki dysków. Można również użyć hello [usługi Kopia zapasowa Azure](/azure/backup/), co pozwoli tooperform możesz automatycznego tworzenia kopii zapasowych podczas hello wirtualna jest uruchomiona.

### <a name="create-snapshot"></a>Tworzenie migawki

Przed utworzeniem migawek dysków maszyny wirtualnej, hello identyfikatora lub nazwy dysku hello jest wymagane. Użyj hello [az maszyny wirtualnej pokazu](https://docs.microsoft.com/en-us/cli/azure/vm#show) identyfikator dysku hello tooreturn polecenia. W tym przykładzie identyfikator dysku hello jest przechowywana w zmiennej, dzięki czemu mogą być używane w kolejnym kroku.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Teraz, gdy masz hello identyfikator dysku maszyny wirtualnej hello hello następujące polecenie tworzy migawkę hello dysku.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Utwórz dysk z migawki

Następnie można przekonwertować tej migawki na dysku, który może być maszyny wirtualnej hello toorecreate używane.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Przywracanie z migawki maszyny wirtualnej

odzyskiwanie maszyny wirtualnej toodemonstrate, Usuń hello istniejącej maszyny wirtualnej. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Utwórz nową maszynę wirtualną na podstawie hello migawki dysku.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Podłącz dysk danych

Wszystkie dyski danych powinny maszyny wirtualnej toohello toobe ponownie nałożona.

Najpierw znaleźć nazwy dysku danych hello przy użyciu hello [Lista dysków az](https://docs.microsoft.com/cli/azure/disk#list) polecenia. W tym przykładzie miejsca hello nazwę dysku hello w zmiennej o nazwie *datadisk*, która jest używana w hello następnego kroku.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Użyj hello [dołączyć dysku maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/disk#attach) polecenia tooattach hello dysku.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono tematy dysków maszyny Wirtualnej takich jak:

> [!div class="checklist"]
> * Dyski systemu operacyjnego i tymczasowego
> * Dyski danych
> * Standard i dysków w warstwie Premium
> * Wydajność dysku
> * Dołączanie i przygotowywania dysków z danymi
> * Zmiana rozmiaru dysków
> * Migawki dysków

Przejdź dalej toolearn samouczka toohello dotyczące automatyzowania konfiguracji maszyny Wirtualnej.

> [!div class="nextstepaction"]
> [Automatyzowanie konfiguracji maszyny wirtualnej](./tutorial-automate-vm-deployment.md)
