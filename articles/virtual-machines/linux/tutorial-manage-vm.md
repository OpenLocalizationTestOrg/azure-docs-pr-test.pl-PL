---
title: "aaaCreate i zarządzanie maszyn wirtualnych systemu Linux z hello Azure CLI | Dokumentacja firmy Microsoft"
description: "Samouczek — tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure

Maszyny wirtualne platformy Azure zawierają w pełni konfigurowalne i elastyczne środowiska komputerowego. Ten samouczek obejmuje elementów wdrożenia podstawowej maszyny wirtualnej platformy Azure, takich jak rozmiar maszyny Wirtualnej, wybierając obrazu maszyny Wirtualnej i wdrażanie maszyny Wirtualnej. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie i łączenie tooa maszyny Wirtualnej
> * Wybierz i używać obrazów maszyn wirtualnych
> * Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych
> * Zmienianie rozmiaru maszyny wirtualnej
> * Wyświetlanie i zrozumienie stanu maszyny Wirtualnej


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia. 

Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Grupy zasobów musi zostać utworzone przed maszyny wirtualnej. W tym przykładzie grupy zasobów o nazwie *myResourceGroupVM* jest tworzony w hello *eastus* regionu. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

Grupa zasobów Hello jest określony, podczas tworzenia lub modyfikowania maszyn wirtualnych, które są widoczne w tym samouczku.

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę wirtualną z hello [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) polecenia. 

Podczas tworzenia maszyny wirtualnej, takich jak obraz systemu operacyjnego, dysku zmiany rozmiaru i administracyjnych poświadczeń jest kilka opcji. W tym przykładzie utworzono maszynę wirtualną o nazwie *myVM* systemem Ubuntu Server. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Raz hello utworzenia maszyny Wirtualnej, hello Azure CLI generuje informacje o hello maszyny Wirtualnej. Zwróć uwagę na powitania `publicIpAddress`, ten adres może być maszyny wirtualnej hello używane tooaccess... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Połącz tooVM

Teraz można podłączyć toohello maszyny Wirtualnej przy użyciu protokołu SSH. Zamień adres IP przykład hello hello `publicIpAddress` zanotowanym w poprzednim kroku hello.

```bash
ssh 52.174.34.95
```

Po zakończeniu hello maszyny Wirtualnej, należy zamknąć sesję SSH hello. 

```bash
exit
```

## <a name="understand-vm-images"></a>Zrozumienie obrazów maszyn wirtualnych

Hello Azure marketplace zawiera wiele obrazów, które mogą być używane toocreate maszyn wirtualnych. W poprzednich krokach hello maszyna wirtualna została utworzona przy użyciu obrazu Ubuntu. W tym kroku powitalne wiersza polecenia platformy Azure jest używane toosearch hello marketplace obrazu CentOS, który jest następnie używany toodeploy drugiej maszyny wirtualnej.  

toosee listę hello najczęściej używane obrazów, użyj hello [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list) polecenia.

```azurecli-interactive 
az vm image list --output table
```

dane wyjściowe polecenia Hello zwraca hello najpopularniejszych obrazów maszyn wirtualnych na platformie Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Pełna lista, można wyświetlić, dodając hello `--all` argumentu. listy obrazów Hello można również filtrować według `--publisher` lub `–-offer`. W tym przykładzie hello lista jest przefiltrowana pod kątem wszystkich obrazów z ofertą, który pasuje *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Częściowe dane wyjściowe:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

toodeploy Maszynę wirtualną przy użyciu określonego obrazu, zanotuj wartość hello w hello *Urn* kolumny. Podczas określania obraz powitania, numer wersji obrazu hello można zastąpić "najnowszej", który wybiera hello najnowszą wersję hello dystrybucji. W tym przykładzie hello `--image` argument jest używany toospecify hello najnowszej wersji obrazu CentOS 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Zrozumienie rozmiarów maszyn wirtualnych

Rozmiar maszyny wirtualnej określa hello zasobów obliczeniowych, takich jak Procesora GPU i pamięci wprowadzone toohello dostępne maszyny wirtualnej. Maszyny wirtualne muszą toobe rozmiary hello oczekiwano obciążenia pracą. Jeśli zwiększa obciążenie, można zmienić rozmiar istniejącej maszyny wirtualnej.

### <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych

w poniższej tabeli Hello kategoryzuje rozmiary do przypadków użycia.  

| Typ                     | Rozmiary           |    Opis       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Zastosowania ogólne](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7| Zrównoważonym Procesora do pamięci. Nadaje się doskonale dla deweloperów / testu i małych toomedium rozwiązania aplikacji i danych.  |
| [Optymalizacja pod kątem obliczeń](sizes-compute.md)   | FS, F             | Wysoka Procesora do pamięci. Nadaje się do aplikacji średnia ruchu, urządzeń sieciowych i procesów wsadowych.        |
| [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Wysoka pamięci do core. Doskonałe rozwiązanie dla relacyjnych baz danych, pamięci podręcznych średnia toolarge i analiza w pamięci.                 |
| [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md)      | Ls                | Wysoka przepływność dysku i operacje we/wy. Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.                                                         |
| [Procesor GPU](sizes-gpu.md)          | WIRTUALIZACJĄ SIECI, NC            | Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych.       |
| [Wysoka wydajność](sizes-hpc.md) | H-A8 11          | Nasze najbardziej zaawansowanych Procesora maszyny wirtualne z interfejsami opcjonalne wysokiej przepustowości sieci (RDMA). 


### <a name="find-available-vm-sizes"></a>Znajdowanie dostępnych rozmiarów maszyny Wirtualnej

toosee listę maszyn wirtualnych rozmiarów dostępnych w określonym regionie, użyj hello [listy rozmiarów maszyn wirtualnych az](/cli/azure/vm#list-sizes) polecenia. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Częściowe dane wyjściowe:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Tworzenie maszyny Wirtualnej o określonym rozmiarze

Witaj poprzedniego przykładu tworzenia maszyny Wirtualnej o rozmiarze nie podano, której wynikiem jest domyślny rozmiar. Można wybrać rozmiar maszyny Wirtualnej za pomocą czasu tworzenia [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i hello `--size` argumentu. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Zmienianie rozmiaru maszyny wirtualnej

Po wdrożeniu maszyny Wirtualnej można tooincrease po zmianie rozmiaru lub zmniejszenia alokacji zasobów.

Przed zmianą rozmiaru maszyny Wirtualnej, sprawdź, czy hello wymagany rozmiar w klastrze jest dostępny hello bieżącej platformy Azure. Witaj [az maszyny wirtualnej-vm — zmiany rozmiaru — opcje listy](/cli/azure/vm#list-vm-resize-options) polecenie zwraca hello listę rozmiarów. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
W razie potrzeby hello się, że rozmiar jest dostępny hello maszyny Wirtualnej można zmienić rozmiar ze stanu zasilania na, jednak podczas hello operacji ponownego rozruchu. Użyj hello [Zmień rozmiar maszyny wirtualnej az]( /cli/azure/vm#resize) zmiany rozmiaru hello tooperform polecenia.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Jeśli hello żądany rozmiar nie jest na powitania bieżący klaster hello wirtualna potrzeb, może wystąpić toobe alokację przed hello operacja zmiany rozmiaru. Użyj hello [deallocate wirtualna az]( /cli/azure/vm#deallocate) polecenia toostop i cofnięcia przydzielenia hello maszyny Wirtualnej. Uwaga: w przypadku hello maszyny Wirtualnej jest włączona ponownie, wszystkie dane na dysku tymczasowym hello mogą zostać usunięte. Hello publiczny adres IP także zmianę, chyba że używana jest statyczny adres IP. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Po cofnięciu przydziału, może wystąpić hello zmiany rozmiaru. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Po hello rozmiaru, można uruchomić hello maszyny Wirtualnej.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>Stany zasilania maszyny Wirtualnej

Maszyny Wirtualnej platformy Azure może mieć jedną z wielu stany zasilania. Ten stan reprezentuje hello bieżący stan hello maszyny Wirtualnej z punktu widzenia hello hello funkcji hypervisor. 

### <a name="power-states"></a>Stany zasilania

| Stan zasilania | Opis
|----|----|
| Uruchamianie | Wskazuje, że jest uruchamiana hello maszyny wirtualnej. |
| Działanie | Wskazuje, że działa hello maszyny wirtualnej. |
| Zatrzymywanie | Wskazuje, że tej maszyny wirtualnej hello jest zatrzymywana. | 
| Zatrzymane | Wskazuje, że tej maszyny wirtualnej hello jest zatrzymana. Maszyny wirtualne w stanie hello zatrzymana nadal naliczenie opłat za obliczenia.  |
| Cofanie przydziału | Wskazuje, że cofana jest hello maszyny wirtualnej. |
| Cofnięcie przydziału | Oznacza, że hello maszyny wirtualnej zostanie usunięty z hello funkcji hypervisor, ale nadal dostępne w płaszczyźnie kontroli hello. Maszyny wirtualne w stanie Deallocated hello nie naliczenie opłat za obliczenia. |
| - | Wskazuje, że stan zasilania hello hello maszyny wirtualnej jest nieznany. |

### <a name="find-power-state"></a>Znajdź stan zasilania

Stan hello tooretrieve określonej maszyny wirtualnej, użyj hello [wirtualna az Pobierz widok wystąpienia](/cli/azure/vm#get-instance-view) polecenia. Należy się toospecify poprawną nazwę maszyny wirtualnej i grupy zasobów. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Dane wyjściowe:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Zadania zarządzania

Podczas hello cyklu maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej. Ponadto można toocreate skrypty tooautomate powtarzających się lub złożonych zadań. Przy użyciu hello Azure CLI, wiele typowych zadań zarządzania można uruchomić z wiersza polecenia hello lub w skryptach. 

### <a name="get-ip-address"></a>Pobierz adres IP

To polecenie zwraca hello prywatnych i publicznych adresów IP maszyny wirtualnej.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Zatrzymaj maszynę wirtualną

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Uruchom maszynę wirtualną

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Usuń grupę zasobów

Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku poznanie podstawowych tworzenia maszyny Wirtualnej i zarządzania, np.:

> [!div class="checklist"]
> * Tworzenie i łączenie tooa maszyny Wirtualnej
> * Wybierz i używać obrazów maszyn wirtualnych
> * Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych
> * Zmienianie rozmiaru maszyny wirtualnej
> * Wyświetlanie i zrozumienie stanu maszyny Wirtualnej

Przejdź dalej toolearn samouczka toohello dysków maszyny Wirtualnej.  

> [!div class="nextstepaction"]
> [Utwórz i Zarządzaj maszyny Wirtualnej dyski](./tutorial-manage-disks.md)
