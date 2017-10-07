---
title: "Szybki Start - aaaAzure utworzyć CLI maszyny Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft"
description: Dowiesz toocreate maszyn wirtualnych systemu Windows z hello wiersza polecenia platformy Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Utwórz maszynę wirtualną systemu Windows z hello wiersza polecenia platformy Azure

Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Szczegóły tego przewodnika przy użyciu hello Azure CLI toodeploy maszyny wirtualnej z systemem Windows Server 2016. Po zakończeniu wdrażania nawiązanie połączenia toohello serwera i zainstaluj usługi IIS.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create). Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). 

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*. W tym przykładzie użyto *azureuser* dla nazwy użytkownika administracyjnego i *myPassword12* jako hello hasła. Zaktualizować te wartości toosomething tooyour odpowiednie środowisko. Te wartości są wymagane podczas tworzenia połączenia z maszyną wirtualną hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. Zwróć uwagę na powitania `publicIpAaddress`. Ten adres jest używany tooaccess hello maszyny Wirtualnej.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Otwieranie portu 80 na potrzeby ruchu w sieci Web 

Domyślnie w tooWindows maszyn wirtualnych wdrożonych w usłudze Azure są dozwolone tylko na połączenia RDP. Jeśli ta maszyna wirtualna będzie toobe serwer sieci Web, należy tooopen port 80 hello Internet. Użyj hello [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) polecenia tooopen hello żądany port.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Podłącz maszynę toovirtual

Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z maszyną wirtualną hello. Zamień adres IP hello hello publiczny adres IP maszyny wirtualnej. Po wyświetleniu monitu wprowadź poświadczenia hello używane podczas tworzenia maszyny wirtualnej hello.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Instalowanie usług IIS przy użyciu programu PowerShell

Teraz, gdy użytkownik zalogował się toohello maszyny Wirtualnej platformy Azure, można użyć pojedynczy wiersz tooinstall PowerShell usług IIS i włączyć ruch internetowy tooallow reguły zapory lokalnej hello. Otwórz wiersz programu PowerShell i uruchom następujące polecenie hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Widok hello strona powitalna usług IIS

Zainstalowane usługi IIS i portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet można użyć przeglądarki sieci web na wybór tooview hello domyślne IIS strony powitalnej. Należy się toouse hello publicznego adresu IP, który opisane powyżej toovisit hello domyślnej strony. 

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web. toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Windows.

> [!div class="nextstepaction"]
> [Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows](./tutorial-manage-vm.md)
