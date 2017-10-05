---
title: Konwertuj zestaw skali maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie skali maszyny wirtualnej systemu Linux Azure ustawiony za pomocą wiersza polecenia platformy Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a>Konwertuj istniejącą maszynę wirtualną platformy Azure na zestaw skali

W tym samouczku przedstawiono sposób używać Azure CLI 2.0 w celu konwertowania maszyny wirtualnej do zestawu skalowania maszyn wirtualnych. Możesz również sposób automatyzowania konfiguracji maszyn wirtualnych w zestawie skalowania. Aby uzyskać więcej informacji na temat sposobu instalowania 2.0 interfejsu wiersza polecenia Azure, zobacz [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawach skali maszyny wirtualnej](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-the-vm"></a>Krok 1 — anulowanie zastrzeżenia maszyny Wirtualnej

Używanie protokołu SSH, aby nawiązać połączenie z maszyną Wirtualną.

Anulowanie zastrzeżenia maszyny Wirtualnej, aby usunąć pliki i dane przy użyciu agenta maszyny Wirtualnej platformy Azure. Szczegółowe omówienie anulowania obsługi, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a>Krok 2 — przechwytywania obrazu maszyny wirtualnej

Aby uzyskać szczegółowe omówienie rejestrowania, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).

Cofnięcie przydziału maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalize maszyny Wirtualnej z [generalize wirtualna az](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Tworzenie obrazu na podstawie zasobu maszyny Wirtualnej z [tworzenia obrazu az](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a>Krok 3 — Utwórz zestaw skali

Pobierz **identyfikator** obrazu.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Utwórz maszynę Wirtualną z zasobu obrazu z [az vmss utworzyć](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

To polecenie również dołączyć dysku danych 10gb. Należy pamiętać, że w zależności od maszyny Wirtualnej wybrany rozmiar (użyliśmy **Standard_DS1_v2**), liczba dysków z danymi dozwolone, jest inny. Aby uzyskać więcej informacji, przejrzyj [rozmiarów maszyn wirtualnych](sizes.md).

Po zakończeniu skali się z nim połączyć. Pobierz listę adresów IP dla wystąpień SSH z [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Teraz możesz nawiązać połączenie wystąpienie maszyny wirtualnej, aby zainicjalizować dysk danych

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a>Krok 4 — zainicjalizować dysk danych

Podczas połączenia z maszyną wirtualną, partycji dysku z `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Zapis systemu plików z partycją `mkfs` polecenia:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Zainstaluj nowy dysk, tak aby była dostępna w systemie operacyjnym:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

Dysk można teraz dostęp za pośrednictwem datadrive punktu instalacji, który można sprawdzić przy `ls /datadrive/`.

Zakończyć sesję SSH.


## <a name="step-5---configure-firewall"></a>Krok 5 — Konfigurowanie zapory

Dziurkowanie przerw za pośrednictwem zapory, serwer sieci Web obsługiwane przez zestaw skali. Podczas tworzenia zestawu skali, usługi równoważenia obciążenia została także utworzona i użyto go **SSH** do poszczególnych maszyn wirtualnych. Aby otworzyć port, potrzebne informacje, którą można uzyskać przy użyciu wiersza polecenia platformy Azure.

* **Pula adresów IP frontonu**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Pula adresów IP zaplecza**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Przy użyciu tych dwóch nazw, należy otworzyć port **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Krok 6 — automatyzowania konfiguracji

Dysk z danymi musi zostać skonfigurowane na każde wystąpienie maszyny wirtualnej. Firma Microsoft można zautomatyzować konfigurację maszyny wirtualnej o **CustomScript** rozszerzenia.

Najpierw utwórz *SH* skryptu, który zawiera polecenia format dysku.

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Następnie przekazywanie tego pliku skryptu do where **CustomScript** rozszerzenia do niego dostęp. Jest dostępna kopia [tutaj](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Tworzenie pliku lokalnego o nazwie **settings.json** i umieszcza w nim następujący blok JSON. `flieUris` Właściwość powinna być ustawiona, gdy plik skryptu została przekazana do.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Wdrożyć na skalę ustawiony za pomocą tego polecenia **CustomScript** rozszerzenia, odwołuje się do **settings.json** właśnie utworzony plik.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

To rozszerzenie automatycznie wykorzystuje wszystkie bieżące wystąpienia i wystąpienia utworzone później przez skalowanie.

## <a name="step-7---configure-autoscale-rules"></a>Krok 7 — Konfigurowanie reguł automatycznego skalowania

Obecnie reguł skalowania automatycznego nie można ustawić w wiersza polecenia platformy Azure. Użyj [portalu Azure](https://portal.azure.com) skonfigurowanie automatycznego skalowania.

## <a name="step-8---management-tasks"></a>Krok 8 - zadania zarządzania

W całym cyklu życia zestawu skalowania konieczne może być Uruchom jedno lub więcej zadań zarządzania. Ponadto może zajść potrzeba tworzenia skryptów automatyzujących różnych zadań cykl życia i interfejsu wiersza polecenia Azure zapewnia szybki sposób wykonywania tych zadań. Poniżej przedstawiono kilka typowych zadań.

### <a name="get-connection-info"></a>Pobierz informacje o połączeniu

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Ustaw liczbę wystąpień (Ręczne skala)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Usuń grupę zasobów

Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej na temat niektóre funkcje zestawu skali maszyny wirtualnej, wprowadzone w tym samouczku, zobacz następujące informacje:

- [Omówienie usługi Azure zestawy skalowania maszyny wirtualnej](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Omówienie usługi Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Sterowaniu przepływem ruchu sieciowego z grup zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md)