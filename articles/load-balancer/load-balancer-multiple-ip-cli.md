---
title: "aaaLoad równoważenia na wielu konfiguracji adresów IP przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszyny wirtualnej za pomocą wiersza polecenia platformy Azure | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a>Obciążenia równoważenia na wielu konfiguracji adresów IP

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [Interfejs wiersza polecenia](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

W tym artykule opisano, jak toouse modułu równoważenia obciążenia Azure z adresem IP wielu adresów na pomocniczym interfejsie sieciowym (NIC). W tym scenariuszu będziemy mieć dwie maszyny wirtualne z systemami Windows, każdy z podstawowym i pomocniczym karty sieciowej. Każdy z hello dodatkowej karty sieciowe mają dwie konfiguracje adresów IP. Każda maszyna wirtualna obsługuje zarówno contoso.com witryn sieci Web, jak i fabrikam.com. Każda witryna sieci Web jest powiązane tooone konfiguracji IP hello na powitania dodatkowej karty sieciowej. Używamy modułu równoważenia obciążenia Azure tooexpose dwa frontonu adresy IP, po jednej dla każdej witryny sieci Web, toodistribute ruchu toohello odpowiednich konfiguracji IP hello witryny sieci Web. W tym scenariuszu używa hello tego samego numeru portu między zarówno frontends, jak i oba adresy IP do puli wewnętrznej bazy danych.

![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo tooload czynności na wielu konfiguracji adresów IP

Wykonaj kroki hello poniżej scenariuszu hello tooachieve opisane w tym artykule:

1. [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) hello wiersza polecenia platformy Azure, wykonując kroki hello w artykule połączonego hello i dziennika do konta platformy Azure.
2. [Utwórz grupę zasobów](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) o nazwie *contosofabrikam* zgodnie z powyższym opisem.

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. [Tworzenie zestawu dostępności](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor Witaj dwie maszyny wirtualne. W tym scenariuszu należy użyć hello następujące polecenie:

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. [Tworzenie sieci wirtualnej](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) o nazwie *myVNet* i podsieć o nazwie *mySubnet*:

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. [Tworzenie usługi równoważenia obciążenia hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o nazwie *mylb*:

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. Utwórz dwa dynamiczne publiczne adresy IP, w przypadku konfiguracji IP frontonu hello z usługi równoważenia obciążenia:

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. Tworzenie frontonu Witaj dwie konfiguracje adresów IP *contosofe* i *fabrikamfe* odpowiednio:

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. Tworzenie zaplecza pule adresów - *contosopool* i *fabrikampool*, [sondowania](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, i reguły - równoważenia obciążenia *HTTPc* i *HTTPf*:

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. Hello uruchom następujące polecenie poniżej, a następnie sprawdź dane wyjściowe hello zbyt[Sprawdź przez moduł równoważenia obciążenia](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) został utworzony prawidłowo:

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. [Tworzenie publicznego adresu IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, i [konta magazynu](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* na pierwszej maszynie wirtualnej VM1, jak pokazano poniżej:

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. [Tworzenie interfejsów sieciowych hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) dla VM1 i dodać drugi konfiguracji adresów IP, *VM1 ipconfig2*, i [utworzyć hello maszyny Wirtualnej](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) w sposób przedstawiony poniżej:

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. Powtórz kroki od 10 11 dla drugiej maszyny Wirtualnej:

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. Na koniec należy skonfigurować zasobów rekordów toopoint toohello odpowiednich frontonu adresu IP DNS hello modułu równoważenia obciążenia. Może hostować domen w usłudze Azure DNS. Aby uzyskać więcej informacji o korzystaniu z usługi Azure DNS z usługi równoważenia obciążenia, zobacz [przy użyciu usługi Azure DNS z innymi usługami Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej na temat sposobu równoważenia obciążenia toocombine usługi na platformie Azure w [przy użyciu usługi równoważenia obciążenia w Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Dowiedz się, jak można używać różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługą równoważenia obciążenia w [dziennika analizy dla usługi równoważenia obciążenia Azure](../load-balancer/load-balancer-monitor-log.md).
