---
title: aaaCreate i przekazywanie wirtualna OpenBSD obrazu tooAzure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello OpenBSD toocreate systemu operacyjnego maszyny wirtualnej platformy Azure za pomocą wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Tworzenie i przekazywanie tooAzure obrazu dysku OpenBSD
W tym artykule opisano, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello OpenBSD systemu operacyjnego. Po wysłaniu, można użyć jej jako toocreate własny obraz maszyny wirtualnej (VM) na platformie Azure za pomocą wiersza polecenia platformy Azure.


## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że hello następujące elementy:

* **Subskrypcja platformy Azure** — Jeśli nie masz konta, możesz utworzyć jedną w zaledwie kilka minut. Jeśli masz subskrypcję MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). W przeciwnym razie Dowiedz się, jak za[utworzyć bezpłatne konto próbne](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure CLI 2.0** — upewnij się, że masz hello najnowszych [Azure CLI 2.0](/cli/azure/install-azure-cli) zainstalowane i zarejestrowane w tooyour konto platformy Azure z [logowania az](/cli/azure/#login).
* **OpenBSD zainstalowanego systemu operacyjnego w pliku VHD** -obsługiwany system operacyjny OpenBSD (w wersji 6.1) musi być zainstalowany tooa wirtualnego dysku twardego. Wiele narzędzi istnieje toocreate pliki VHD. Można na przykład, takich jak plik VHD hello toocreate funkcji Hyper-V za pomocą rozwiązania wirtualizacji i zainstaluj system operacyjny hello. Aby uzyskać instrukcje dotyczące sposobu tooinstall i użyj funkcji Hyper-V, zobacz [Instalowanie funkcji Hyper-V i tworzenie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Przygotowywanie obrazu OpenBSD dla platformy Azure
Na powitania maszyny Wirtualnej, w którym zainstalowano hello OpenBSD systemie operacyjnym 6.1, w którym dodano obsługę funkcji Hyper-V, wykonaj hello następujące procedury:

1. Jeśli protokół DHCP nie jest włączony podczas instalacji, włącz usługę hello w następujący sposób:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Konfigurowanie konsoli szeregowej w następujący sposób:

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Instalacja pakietu należy skonfigurować w następujący sposób:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. Domyślnie program hello `root` użytkownik jest wyłączony na maszynach wirtualnych platformy Azure. Użytkownicy mogą uruchamiać polecenia z podwyższonym poziomem uprawnień przy użyciu hello `doas` na OpenBSD maszyny Wirtualnej. Doas jest domyślnie włączona. Aby uzyskać więcej informacji, zobacz [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Zainstaluj i skonfiguruj wymagania wstępne dotyczące hello Azure agenta w następujący sposób:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. najnowszą wersję Hello hello Azure agenta zawsze można znaleźć w [Github](https://github.com/Azure/WALinuxAgent/releases). Zainstaluj agenta hello w następujący sposób:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Po zainstalowaniu agenta platformy Azure jest tooverify dobrym rozwiązaniem, która działa w następujący sposób:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Deprovision hello tooclean systemu go i udostępnić go odpowiednie dla reprovisioning. Witaj następujące polecenie spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie i hello skojarzone dane:

    ```sh
    waagent -deprovision+user -force
    ```

Teraz można zamknąć maszyny Wirtualnej.


## <a name="prepare-hello-vhd"></a>Przygotowanie hello wirtualnego dysku twardego
Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**. Możesz przekonwertować hello dysku toofixed formatu wirtualnego dysku twardego za pomocą Menedżera funkcji Hyper-V lub hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) polecenia cmdlet. Przykładem jest następujące.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Utwórz zasoby magazynu i przekaż
Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload dysk VHD, Utwórz konto magazynu z [Tworzenie konta magazynu az](/cli/azure/storage/account#create). Nazwy konta magazynu musi być unikatowa, więc podać własną nazwę. Witaj poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol uzyskać dostęp do konta magazynu toohello, uzyskać klucza magazynu hello z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list) w następujący sposób:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

oddzielne hello toologically wirtualne dyski twarde można przekazać utworzyć kontener w ramach konta magazynu hello z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Na koniec, Przekaż dysk VHD o [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload) w następujący sposób:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Tworzenie maszyny Wirtualnej z dysk VHD
Można utworzyć maszyny Wirtualnej z [przykładowy skrypt](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) lub bezpośrednio z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). toospecify hello OpenBSD wirtualnego dysku twardego został przekazany, użyj hello `--image` parametru w następujący sposób:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Uzyskaj adres IP powitania dla maszyny Wirtualnej z OpenBSD [az vm--adresy ip](/cli/azure/vm#list-ip-addresses) w następujący sposób:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

Teraz można tooyour SSH maszyny Wirtualnej OpenBSD normal:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat funkcji Hyper-V obsługuje na OpenBSD6.1 tooknow należy odczytać [OpenBSD 6.1](https://www.openbsd.org/61.html) i [hyperv.4](http://man.openbsd.org/hyperv.4).

Chcąc toocreate Maszynę wirtualną od dysków zarządzanych, przeczytaj [dysku az](/cli/azure/disk). 
