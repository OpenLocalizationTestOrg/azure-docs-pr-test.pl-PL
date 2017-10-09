---
title: "Moduł równoważenia - obciążenia aaaCreate internetowy, wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia w Menedżerze zasobów przy użyciu hello wiersza polecenia platformy Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Tworzenie usługi równoważenia obciążenia internet przy użyciu hello wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu klasycznego wdrożenia obciążenia toocreate umożliwiających dostęp z Internetu](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Wdrażanie rozwiązania hello przy użyciu hello wiersza polecenia platformy Azure

Witaj następujące kroki pokazują, jak toocreate Internetem obciążenia przy użyciu usługi Azure Resource Manager z interfejsu wiersza polecenia usługi równoważenia. Z usługi Azure Resource Manager wszystkie zasoby, zostało utworzone i skonfigurowane osobno, następnie opracować toocreate zasobu.

Należy utworzyć i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:

* Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.
* Pula adresów zaplecza — zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.
* Reguły równoważenia obciążenia — zawiera reguły mapowania port publiczny na tooport usługi równoważenia obciążenia hello hello puli adresów zaplecza.
* Reguły NAT dla ruchu przychodzącego — zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.
* Sondy — zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.

Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

## <a name="set-up-cli-toouse-resource-manager"></a>Konfigurowanie toouse interfejsu wiersza polecenia Menedżera zasobów

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **trybie azure config** tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.

    ```azurecli
        azure config mode arm
    ```

    Oczekiwane dane wyjściowe:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Tworzenie sieci wirtualnej i publiczny adres IP dla puli adresów IP frontonu hello

1. Utwórz sieć wirtualną (VNet) o nazwie *NRPVnet* w lokalizacji wschodnie stany USA hello za pomocą grupy zasobów o nazwie *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Utwórz podsieć o nazwie *NRPVnetSubnet* z blokiem CIDR 10.0.0.0/24 w sieci *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Utwórz publiczny adres IP o nazwie *NRPPublicIP* toobe używane przez pulę IP frontonu z nazwą DNS *loadbalancernrp.eastus.cloudapp.azure.com*. poniższe polecenie hello używa hello alokacji statycznych typu i limit czasu bezczynności 4 minut.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > usługi równoważenia obciążenia Hello użyje hello etykieta domeny publicznego adresu IP hello jako nazwy FQDN. Ta zmiana wdrożenie klasyczne, używa usługi w chmurze hello hello równoważenia obciążenia w pełni kwalifikowanej domeny nazwę (FQDN).
   > W tym przykładzie hello nazwy FQDN jest *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Tworzenie modułu równoważenia obciążenia

Witaj poniższe polecenie tworzy moduł równoważenia obciążenia o nazwie *NRPlb* w hello *NRPRG* grupy zasobów w hello *wschodnie stany USA* lokalizacji platformy Azure.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Tworzenie puli adresów IP frontonu i puli adresów zaplecza
W tym przykładzie pokazano, jak toocreate hello frontonu puli adresów IP odbierająca hello przychodzącego ruchu sieciowego na powitania modułu równoważenia obciążenia i hello puli adresów IP zaplecza, gdzie puli frontonu hello wysyła ruch sieciowy hello ze zrównoważonym obciążeniem.

1. Utwórz pulę IP frontonu skojarzenie publicznego adresu IP hello utworzone w poprzednim kroku hello i hello modułu równoważenia obciążenia.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Skonfiguruj pulę adresów zaplecza używane tooreceive ruch przychodzący z puli adresów IP frontonu hello.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>Tworzenie reguł równoważenia obciążenia, reguł NAT oraz sond

W tym przykładzie tworzy hello następujące elementy.

* translator NAT reguły tootranslate cały ruch przychodzący na porcie 21 tooport 22<sup>1</sup>
* translator NAT reguły tootranslate cały ruch przychodzący na porcie 23 tooport 22
* toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresów w puli zaplecza hello.
* stan kondycji sondowania reguł toocheck hello na stronie o nazwie *HealthProbe.aspx*.

<sup>1</sup> reguł NAT są skojarzone tooa wystąpienia określonej maszyny wirtualnej za hello równoważenia obciążenia. ruch sieciowy Hello przychodzące do portu 21 są wysyłane tooa określonej maszyny wirtualnej na porcie 22 skojarzone z tą regułą translatora adresów Sieciowych. Musisz określić protokół (UDP lub TCP) dla reguły NAT. Oba protokoły nie może być przypisana toohello tego samego portu.

1. Tworzenie reguł NAT hello.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Utwórz regułę modułu równoważenia obciążenia.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Utwórz sondę kondycji.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Sprawdź ustawienia.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Oczekiwane dane wyjściowe:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>Tworzenie kart sieciowych

Należy toocreate karty sieciowe (lub modyfikować istniejące) i kojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sondy.

1. Utwórz kartę Sieciową o nazwie *można nic1 lb*i skojarz go z hello *rdp1* NAT reguły i hello *NRPbackendpool* puli adresów zaplecza.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
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

2. Utwórz kartę Sieciową o nazwie *można nic2 lb*i skojarz go z hello *rdp2* NAT reguły i hello *NRPbackendpool* puli adresów zaplecza.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Utwórz maszynę wirtualną (VM) o nazwie *web1*i skojarz go z hello karty Sieciowej o nazwie *można nic1 lb*. Konto magazynu o nazwie *web1nrp* został utworzony przed uruchomieniem polecenia hello poniżej.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Maszyny wirtualne w toobe potrzeby modułu równoważenia obciążenia, w hello tego samego zestawu dostępności. Użyj `azure availset create` toocreate zestawu dostępności.

    Hello dane wyjściowe powinny być podobne toohello następujące czynności:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > komunikat informacyjny Hello **jest karta sieciowa bez publicznego adresu IP skonfigurowanych** oczekuje się od chwili utworzenia hello NIC dla usługi równoważenia obciążenia hello łączenie tooInternet przy użyciu hello adres usługi równoważenia obciążenia publicznego adresu IP.

    Od hello *można nic1 lb* kart interfejsu Sieciowego jest skojarzony z hello *rdp1* reguły NAT można się połączyć za*web1* za pomocą protokołu RDP za pośrednictwem portu 3441 na powitania modułu równoważenia obciążenia.

4. Utwórz maszynę wirtualną (VM) o nazwie *sieci Web 2*i skojarz go z hello karty Sieciowej o nazwie *można nic2 lb*. Konto magazynu o nazwie *web1nrp* został utworzony przed uruchomieniem polecenia hello poniżej.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Aktualizowanie istniejącego modułu równoważenia obciążenia
Możesz dodać reguły odwołujące się do istniejącego modułu równoważenia obciążenia. W następnym przykładzie hello, nowe reguły modułu równoważenia obciążenia jest dodawany tooan istniejący moduł równoważenia obciążenia **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Usuwanie modułu równoważenia obciążenia
Użyj hello następujące polecenia tooremove modułu równoważenia obciążenia:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Następne kroki
[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
