---
title: aaaConvert Azure tooa zestawu skalowania maszyny wirtualnej | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie skali maszyny wirtualnej systemu Linux Azure ustawiony za pomocą hello Azure CLI."
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
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Konwertuj istniejącego zestawu skalowania maszyny wirtualnej platformy Azure tooa

Ten samouczek pokazuje, jak tooconvert toouse Azure CLI 2.0 tooa maszyny wirtualnej zestawu skalowania maszyn wirtualnych. Możesz też dowiedzieć się, jak tooautomate hello hello maszyn wirtualnych w skali hello konfiguracja. Aby uzyskać więcej informacji na temat tooinstall Azure CLI 2.0, zobacz temat [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawach skali maszyny wirtualnej](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Krok 1 - Deprovision hello maszyny Wirtualnej

Użyj toohello tooconnect SSH maszyny Wirtualnej.

Witaj deprovision maszyny Wirtualnej przy użyciu hello Azure VM agent toodelete plików i danych. Szczegółowe omówienie anulowania obsługi, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Krok 2 — Przechwyć obraz powitania maszyny Wirtualnej

Aby uzyskać szczegółowe omówienie rejestrowania, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).

Cofnięcie przydziału hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalize hello maszyny Wirtualnej z [generalize wirtualna az](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Tworzenie obrazu na podstawie hello zasobu maszyny Wirtualnej z [tworzenia obrazu az](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Krok 3 — Tworzenie hello zestaw skali

Pobierz hello **identyfikator** hello obrazu.

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

To polecenie również dołączyć dysku danych 10gb. Należy pamiętać, że w zależności od hello maszyny Wirtualnej wybrany rozmiar (użyliśmy **Standard_DS1_v2**), hello liczba dysków z danymi dozwolone jest różna. Aby uzyskać więcej informacji, przejrzyj hello [rozmiarów maszyn wirtualnych](sizes.md).

Po zakończeniu zestawu skalowania hello, należy połączyć tooit. Pobierz listę adresów IP dla wystąpień hello SSH z [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Teraz można podłączyć dysku danych hello wystąpienia tooinitialize toohello maszyny wirtualnej

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Krok 4 — dysk danych hello inicjowania

Podczas połączenia toohello maszyny wirtualnej, partycji dysku hello `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Zapis partycji toohello systemu plików z hello `mkfs` polecenia:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Zainstaluj nowy dysk hello tak, aby była dostępna w systemie operacyjnym hello:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

Witaj dysku może być teraz dostęp za pośrednictwem punktu instalacji datadrive hello, które można sprawdzić przy `ls /datadrive/`.

Zakończyć sesję SSH hello.


## <a name="step-5---configure-firewall"></a>Krok 5 — Konfigurowanie zapory

Dziurkowanie przerw za pośrednictwem hello zapory toohello serwer sieci Web: obsługiwane przez zestaw skali hello. Podczas tworzenia zestawu skali hello, modułu równoważenia obciążenia została także utworzona i użyto go **SSH** toohello poszczególnych maszyn wirtualnych. tooopen portu, potrzebne informacje, którą można uzyskać przy użyciu wiersza polecenia platformy Azure.

* **Pula adresów IP frontonu**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Pula adresów IP zaplecza**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Przy użyciu tych dwóch nazw, należy otworzyć port **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Krok 6 — automatyzowania konfiguracji

Hello dysk danych wymaga toobe skonfigurowane na każde wystąpienie maszyny wirtualnej. Firma Microsoft można zautomatyzować hello konfiguracji maszyny wirtualnej hello z hello **CustomScript** rozszerzenia.

Najpierw utwórz *SH* skryptu, który zawiera polecenia format dysku hello.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Następnie przekaż tego hello toowhere pliku skryptu **CustomScript** rozszerzenia do niego dostęp. Jest dostępna kopia [tutaj](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Tworzenie pliku lokalnego o nazwie **settings.json** i put hello po bloku JSON w nim. Witaj `flieUris` można ustawić właściwości toowhere przekazany do pliku skryptu.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Wdrażanie tej skali tooyour polecenia ustawiony za pomocą hello **CustomScript** rozszerzenia odwołujące się do hello **settings.json** właśnie utworzony plik.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

To rozszerzenie automatycznie wykorzystuje wszystkie bieżące wystąpienia i wystąpienia utworzone później przez skalowanie.

## <a name="step-7---configure-autoscale-rules"></a>Krok 7 — Konfigurowanie reguł automatycznego skalowania

Obecnie reguł skalowania automatycznego nie można ustawić w wiersza polecenia platformy Azure. Użyj hello [portalu Azure](https://portal.azure.com) tooconfigure automatycznego skalowania.

## <a name="step-8---management-tasks"></a>Krok 8 - zadania zarządzania

W całym cyklu życia hello zestawu skali hello, może być konieczne toorun jednego lub więcej zadań zarządzania. Ponadto może ma skrypty toocreate, które automatyzują różnych zadań cyklu życia i hello interfejsu wiersza polecenia Azure udostępnia toodo szybko tych zadań. Poniżej przedstawiono kilka typowych zadań.

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
więcej informacji na temat niektórych hello skalowania maszyny wirtualnej ustawić funkcje wprowadzone w tym samouczku toolearn Zobacz hello następujących informacji:

- [Omówienie usługi Azure zestawy skalowania maszyny wirtualnej](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Omówienie usługi Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Sterowaniu przepływem ruchu sieciowego z grup zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md)