---
title: "Moduł równoważenia - obciążenia aaaCreate wewnętrzne, wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wewnętrznego modułu równoważenia obciążenia przy użyciu hello interfejsu wiersza polecenia Azure Resource Manager"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello wewnętrznego modułu równoważenia obciążenia

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Wdrażanie rozwiązania hello przy użyciu hello wiersza polecenia platformy Azure

Witaj następujące kroki pokazują, jak toocreate internetowy modułu równoważenia obciążenia za pomocą interfejsu wiersza polecenia przy użyciu usługi Azure Resource Manager. Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, a następnie umieść razem toocreate zasobu.

Należy toocreate i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:

* **Konfiguracja adresu IP frontonu** — publiczne adresy IP dla przychodzącego ruchu sieciowego.
* **Pula adresów zaplecza**: zawiera interfejsów sieciowych (NIC), które umożliwiają ruch sieciowy tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia
* **Reguły równoważenia obciążenia**: zawiera reguły, które mapują port publiczny na tooport usługi równoważenia obciążenia hello w puli adresów zaplecza hello
* **Reguły NAT dla ruchu przychodzącego**: zawiera reguły, które mapują port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello
* **Sondy**: zawiera sondy kondycji, które są używane toocheck hello dostępność wystąpień maszyn wirtualnych w puli adresów zaplecza hello

Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

## <a name="set-up-cli-toouse-resource-manager"></a>Konfigurowanie toouse interfejsu wiersza polecenia Menedżera zasobów

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [zainstalować i skonfigurować hello Azure CLI](../cli-install-nodejs.md). Wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **trybie azure config** polecenia tooswitch tooResource Menedżera tryb, w następujący sposób:

    ```azurecli
    azure config mode arm
    ```

    Oczekiwane dane wyjściowe:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Tworzenie wewnętrznego modułu równoważenia obciążenia krok po kroku

1. Zaloguj się tooAzure.

    ```azurecli
    azure login
    ```

    Po wyświetleniu monitu wprowadź swoje poświadczenia platformy Azure.

2. Zmień tryb usługi Resource Manager tooAzure hello polecenia narzędzia.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Wszystkie zasoby usługi Azure Resource Manager są kojarzone z grupą zasobów. Jeśli jeszcze nie wykonano tej czynności, utwórz grupę zasobów.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Tworzenie zestawu wewnętrznego modułu równoważenia obciążenia

1. Utwórz wewnętrzny moduł równoważenia obciążenia.

    W następujących scenariuszy hello grupy zasobów o nazwie nrprg jest tworzony w regionie wschodnie stany USA.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Wszystkie zasoby wewnętrzne moduły równoważenia obciążenia, takich jak sieci wirtualnych i podsieci sieci wirtualnej, musi być w hello tej samej grupie zasobów i w hello sam region.

2. Utwórz adres IP frontonu w hello wewnętrznego modułu równoważenia obciążenia.

    użyty adres IP Hello musi być w zakresie hello podsieci sieci wirtualnej.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Utwórz pulę adresów zaplecza hello.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Po zdefiniowaniu adresu IP frontonu i puli adresów zaplecza możesz utworzyć reguły modułu równoważenia obciążenia, reguły NAT dla ruchu przychodzącego i dostosowane sondy kondycji.

4. Utwórz reguły modułu równoważenia obciążenia dla hello wewnętrznego modułu równoważenia obciążenia.

    Po wykonaniu poprzednich kroków hello hello polecenie tworzy regułę równoważenia obciążenia dla nasłuchiwania tooport 1433 hello puli frontonu i wysyłania równoważeniem obciążenia ruchu toohello zaplecza puli adresów sieciowych, również przy użyciu portu 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Utwórz reguły NAT dla ruchu przychodzącego.

    Reguły ruchu przychodzącego translatora adresów Sieciowych są używane toocreate punkty końcowe w moduł równoważenia obciążenia wykraczające tooa wystąpienia określonej maszyny wirtualnej. poprzednie kroki Hello utworzone dwie reguły NAT dla pulpitu zdalnego.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Utwórz sondy kondycji dla usługi równoważenia obciążenia hello.

    Sondy kondycji sprawdza wszystkie toomake wystąpień maszyny wirtualnej się, że może wysyłać ruch w sieci. Hello wystąpienie maszyny wirtualnej z sondy nie powiodło się sprawdzenie zostanie usunięty z modułu równoważenia obciążenia hello dopiero po jej przejdzie do trybu online i sprawdź sondowania Określa, że jest w dobrej kondycji.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > platformy Microsoft Azure Hello używa statycznych, publicznie routingu adresów IPv4 dla różnych scenariuszy administracyjnych. adres IP Hello jest 168.63.129.16. Ten adres IP nie powinien być blokowany przez zapory, ponieważ może to spowodować nieoczekiwane zachowanie.
    > Równoważenia obciążenia wewnętrznego tooAzure względem ten adres IP jest używana przez monitorowanie sond z stan kondycji hello toodetermine usługi równoważenia obciążenia hello maszyn wirtualnych w zestawie o zrównoważonym obciążeniu. Jeśli grupa zabezpieczeń sieci jest toorestrict używanych maszyn wirtualnych tooAzure ruchu w zestawie wewnętrznie równoważeniem obciążenia lub zastosowane tooa podsieć sieci wirtualnej, upewnij się, że reguły zabezpieczeń sieci został dodany ruchu tooallow 168.63.129.16.

## <a name="create-nics"></a>Tworzenie kart sieciowych

Należy toocreate karty sieciowe (lub modyfikować istniejące) i kojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sondy.

1. Utwórz kartę Sieciową o nazwie *można nic1 lb*i skojarz ją z hello *rdp1* NAT reguły i hello *beilb* puli adresów zaplecza.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    Oczekiwane dane wyjściowe:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Utwórz kartę Sieciową o nazwie *można nic2 lb*i skojarz ją z hello *rdp2* NAT reguły i hello *beilb* puli adresów zaplecza.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Utwórz maszynę wirtualną o nazwie *DB1*i skojarz ją z hello karty Sieciowej o nazwie *można nic1 lb*. Konto magazynu o nazwie *web1nrp* jest utworzony przed powitania po uruchomieniu polecenia:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Maszyny wirtualne w toobe potrzeby modułu równoważenia obciążenia, w hello tego samego zestawu dostępności. Użyj `azure availset create` toocreate zestawu dostępności.

4. Utwórz maszynę wirtualną (VM) o nazwie *bazy danych DB2*i skojarz ją z hello karty Sieciowej o nazwie *można nic2 lb*. Konto magazynu o nazwie *web1nrp* został utworzony przed uruchomieniem hello następujące polecenia.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Usuwanie modułu równoważenia obciążenia

tooremove modułu równoważenia obciążenia, hello Użyj następującego polecenia:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Następne kroki

[Configure a load balancer distribution mode by using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)

