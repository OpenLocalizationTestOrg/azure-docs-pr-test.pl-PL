---
title: aaaAzure Szybki Start - CLI tworzenia maszyny Wirtualnej | Dokumentacja firmy Microsoft
description: Dowiesz toocreate maszyn wirtualnych z hello wiersza polecenia platformy Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Utwórz maszynę wirtualną systemu Linux z hello wiersza polecenia platformy Azure

Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Szczegóły ten przewodnik przy użyciu hello Azure CLI toodeploy maszyny wirtualnej z systemem Ubuntu server. Po wdrożeniu serwera hello połączenia SSH jest tworzony, i NGINX, serwer sieci Web jest zainstalowana.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. 

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* i tworzy kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza. toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. Zwróć uwagę na powitania `publicIpAddress`. Ten adres jest używany tooaccess hello maszyny Wirtualnej.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Otwieranie portu 80 na potrzeby ruchu w sieci Web 

Domyślnie dozwolone są tylko połączenia SSH z maszynami wirtualnymi z systemem Linux wdrożonymi na platformie Azure. Jeśli ta maszyna wirtualna będzie toobe serwer sieci Web, należy tooopen port 80 hello Internet. Użyj hello [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) polecenia tooopen hello żądany port.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>Łączenie z maszyną wirtualną za pośrednictwem protokołu SSH

Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello. Upewnij się, że tooreplace  *<publicIpAddress>*  z hello Popraw publiczny adres IP maszyny wirtualnej.  W naszym powyższym przykładzie adres IP to *40.68.254.142*.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>Instalowanie serwera NGINX

Użyj następujących hello bash źródła pakietów tooupdate skryptu i zainstaluj najnowszy pakiet NGINX hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Wyświetlanie hello NGINX strony powitalnej

NGINX zainstalowane i numer portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet — można użyć przeglądarki sieci web na wybór tooview hello domyślne NGINX strony powitalnej. Należy się hello toouse *publicznego adresu IP* opisane powyżej toovisit hello domyślnej strony. 

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web. toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Linux.


> [!div class="nextstepaction"]
> [Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux](./tutorial-manage-vm.md)
