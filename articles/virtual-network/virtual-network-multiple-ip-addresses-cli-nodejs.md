---
title: "aaaVM z wielu adresów IP przy użyciu hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszynę wirtualną przy użyciu hello Azure CLI 1.0 | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Przypisz wielu adresów IP maszyn toovirtual przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

W tym artykule opisano, jak toocreate maszynę wirtualną (VM) za pośrednictwem hello Azure Resource Manager deployment model przy użyciu hello Azure CLI w wersji 1.0. Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania. więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP

Można wykonać tego zadania przy użyciu hello Azure CLI 1.0 (w tym artykule) lub hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md). Hello przestrzeganie objaśniono sposób toocreate przykład maszynę Wirtualną za pomocą wielu IP adresów, zgodnie z opisem w scenariuszu hello. Zmień nazwy zmiennych i typy adresów IP zgodnie z wymaganiami implementacji.

1. Instalowanie i konfigurowanie hello Azure CLI 1.0 przez hello następujące kroki w hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu i zaloguj się do konta platformy Azure z hello `azure-login` polecenia.

2. Utwórz grupę zasobów:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Utwórz sieć wirtualną:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Utwórz podsieć w sieci wirtualnej hello:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Utwórz konto magazynu dla hello maszyny Wirtualnej. Przed uruchomieniem hello następujące polecenia, Zastąp *mojekontomagazynu* o unikatowej nazwie. Nazwa Hello musi być unikatowa w obrębie platformy Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Utwórz hello konfiguracje adresów IP, karty Sieciowej i przypisz hello IP konfiguracje toohello karty sieciowej. Można dodać, usunąć lub zmienić konfigurację hello w razie potrzeby. w scenariuszu hello opisano Hello następujące konfiguracje:

    **Polecenie IPConfig-1**

    Wprowadź hello poleceń, które należy wykonać toocreate:

    - Publiczny zasobu adresu IP za pomocą statycznego publicznego adresu IP
    - Karta sieciowa, przypisywanie hello publicznego adresu IP i statyczne tooit prywatnego adresu IP.
    
    Zastąp *mypublicdns* o nazwie, która jest unikatowa w hello lokalizacji platformy Azure.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.

    **Polecenie IPConfig-2**

     Wprowadź następujące polecenia toocreate hello nowy zasób publiczny adres IP i nową konfigurację adresu IP z statycznego publicznego adresu IP i statycznego prywatnego adresu IP:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **Polecenie IPConfig 3**

    Wprowadź hello następujące polecenia toocreate konfigurację protokołu IP z statycznego prywatnego adresu IP i nie publiczny adres IP:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Chociaż ten artykuł przypisuje wszystkie tooa konfiguracji IP jednej karty Sieciowej, można przypisać wielu tooany konfiguracji adresu IP karty Sieciowej na maszynie wirtualnej. toolearn sposób odczytać Maszynę wirtualną z wieloma kartami sieciowymi, toocreate hello Utwórz maszynę Wirtualną z wielu kart sieciowych artykułu.

7. Tworzenie maszyny wirtualnej z systemem Linux 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello v2 tooStandard DS2 rozmiar maszyny Wirtualnej, na przykład po prostu dodaj następujące właściwości hello `--vm-size Standard_DS3_v2` toohello `azure vm create` polecenia w kroku 6.

8. Wprowadź hello następujące polecenia tooview hello karty Sieciowej i hello skojarzone konfiguracje adresów IP:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.

## <a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej

Możesz dodać dodatkowe prywatnych i publicznych IP adresów tooan istniejących kart interfejsu Sieciowego, wykonując kroki hello, które należy wykonać. Przykłady Hello zależą od hello [scenariusza](#Scenario) opisane w tym artykule.

1. Otwórz okno wiersza polecenia platformy Azure i pełne hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji interfejsu wiersza polecenia. Jeśli nie masz jeszcze interfejsu wiersza polecenia Azure zainstalowany i skonfigurowany, pełną hello etapami hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu i zaloguj się do konta platformy Azure.

2. Wykonaj kroki hello w jednym z następujących sekcji, w zależności od wymagań hello:

    - **Dodaj prywatnego adresu IP**
    
        tooadd prywatnej tooa adresu IP karty Sieciowej, należy utworzyć konfigurację protokołu IP przy użyciu poniższego polecenia hello. statyczny adres Hello musi zawierać adres nieużywane hello podsieci.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).

    - **Dodaj publiczny adres IP**
    
        Publiczny adres IP zostanie dodany przez skojarzenie tooeither nową konfigurację adresu IP lub istniejącej konfiguracji adresu IP. Wykonaj kroki hello w jednym z hello kolejnych sekcjach, ile potrzebujesz.

        > [!NOTE]
        > Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.
        >

        **Skojarz hello zasobów tooa nową konfigurację IP**
    
        Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP. Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową. toocreate nową, wprowadź następujące polecenie hello:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        toocreate nowej konfiguracji IP przy użyciu statycznego prywatnego adresu IP i hello skojarzone *myPublicIP3* publicznego adresu IP adresów zasobów, wpisz następujące polecenie hello:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Skojarz hello zasobów tooan istniejącej konfiguracji IP**

        Zasób publicznego adresu IP może być tylko skojarzone tooan konfiguracji adresów IP, który nie ma jeszcze skojarzone. Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie hello:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Wyszukaj toohello podobne wiersza, który wykonuje 3 IPConfig w hello zwrócone dane wyjściowe:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Ponieważ hello **publicznego adresu IP** kolumny dla *IpConfig 3* jest puste, zasobu bez publicznego adresu IP jest obecnie skojarzone tooit. Można dodać istniejącego publicznego adresu IP adres zasobów tooIpConfig-3, lub wprowadź powitania po toocreate polecenia, co:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Wprowadź następujące polecenie publicznego adresu IP tooassociate hello adresów zasobów toohello istniejącej konfiguracji IP o nazwie hello *IPConfig 3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Wyświetlanie hello prywatnych adresów IP i hello publicznego adresu IP adres zasobów przypisanych toohello hello karty Sieciowej, wprowadzając następujące polecenie:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Hello zwrócił dane wyjściowe są podobne toohello następujące czynności:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Dodaj hello prywatnych adresów IP systemu operacyjnego maszyny Wirtualnej toohello kart toohello dodane przez instrukcjami hello w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
