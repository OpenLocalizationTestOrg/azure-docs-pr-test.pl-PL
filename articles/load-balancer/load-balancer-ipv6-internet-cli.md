---
title: "Moduł równoważenia obciążenia aaaCreate internetowy z IPv6 - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia w przypadku adresu IPv6 za pomocą usługi Azure Resource Manager hello wiersza polecenia platformy Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Tworzenie modułu równoważenia obciążenia z protokołu IPv6 w usłudze Azure Resource Manager przy użyciu interfejsu wiersza polecenia Azure hello internetowy

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](load-balancer-ipv6-internet-cli.md)
> * [Szablon](load-balancer-ipv6-internet-template.md)

Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP). Hello modułu równoważenia obciążenia zapewnia wysoką dostępność, przekazując przychodzący ruch między wystąpienie usługi działa prawidłowo usług w chmurze lub maszyn wirtualnych w zestawie usługi równoważenia obciążenia. Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.

## <a name="example-deployment-scenario"></a>Przykładowy scenariusz wdrażania

Witaj poniższym diagramie przedstawiono rozwiązania do równoważenia obciążenia hello wdrażane za pomocą szablonu przykład hello opisane w tym artykule.

![Scenariusz modułu równoważenia obciążenia](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

W tym scenariuszu utworzysz hello następujących zasobów platformy Azure:

* dwóch maszyn wirtualnych (VM)
* Interfejs sieci wirtualnej, dla każdej maszyny Wirtualnej przy użyciu adresów IPv4 i IPv6 przypisany
* Moduł równoważenia obciążenia internetowy z protokołów IPv4 i IPv6 publicznego adresu IP
* toothat zestawu dostępności zawiera Witaj dwie maszyny wirtualne
* dwa załadować równoważenia reguły toomap hello publiczne adresy VIP toohello prywatnej punkty końcowe

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Wdrażanie rozwiązania hello przy użyciu hello wiersza polecenia platformy Azure

Witaj następujące kroki pokazują, jak toocreate Internetem obciążenia przy użyciu usługi Azure Resource Manager z interfejsu wiersza polecenia usługi równoważenia. Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, a następnie umieść razem toocreate zasobu.

toodeploy modułu równoważenia obciążenia, możesz utworzyć i skonfigurować hello następujące obiekty:

* Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.
* Pula adresów zaplecza — zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.
* Reguły równoważenia obciążenia — zawiera reguły mapowania port publiczny na tooport usługi równoważenia obciążenia hello hello puli adresów zaplecza.
* Reguły NAT dla ruchu przychodzącego — zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.
* Sondy — zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.

Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Konfigurowanie sieci toouse środowiska interfejsu wiersza polecenia usługi Azure Resource Manager

Na przykład Uruchamiamy hello narzędzi interfejsu wiersza polecenia w oknie poleceń programu PowerShell. Nie użyto polecenia cmdlet programu Azure PowerShell hello, ale używamy czytelność tooimprove możliwości i ponowne użycie skryptów programu PowerShell w.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **trybie azure config** tryb Manager tooResource tooswitch polecenia.

    ```azurecli
    azure config mode arm
    ```

    Oczekiwane dane wyjściowe:

        info:    New mode is arm

3. Zaloguj się tooAzure i uzyskać listę subskrypcji.

    ```azurecli
    azure login
    ```

    Wprowadź swoje poświadczenia usługi Azure, po wyświetleniu monitu.

    ```azurecli
    azure account list
    ```

    Wybierz subskrypcję hello, który ma toouse. Zanotuj identyfikator subskrypcji hello hello następnego kroku.

4. Ustawianie zmiennych środowiska PowerShell do użytku z hello polecenia interfejsu wiersza polecenia.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Utwórz grupę zasobów, usługi równoważenia obciążenia sieci wirtualnej i podsieci

1. Tworzenie grupy zasobów

    ```azurecli
    azure group create $rgName $location
    ```

2. Tworzenie modułu równoważenia obciążenia

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Utwórz sieć wirtualną (VNet).

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Utwórz dwie podsieci w tej sieci wirtualnej.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Tworzenie publicznych adresów IP dla puli frontonu hello

1. Ustawianie zmiennych środowiska PowerShell hello

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Utwórz publiczny pulę adresów IP hello frontonu IP.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > Moduł równoważenia obciążenia Hello używa hello etykieta domeny publicznego adresu IP hello jako nazwy FQDN. Ta zmiana wdrożenie klasyczne, używający nazwa usługi w chmurze hello hello równoważenia obciążenia w pełni kwalifikowaną nazwę domeny.
    > W tym przykładzie hello nazwy FQDN jest *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Tworzenie puli frontonu i zaplecza

W tym przykładzie tworzy hello frontonu puli adresów IP odbierająca hello przychodzącego ruchu sieciowego na powitania modułu równoważenia obciążenia i puli adresów IP zaplecza hello gdzie puli frontonu hello wysyła ruch sieciowy hello ze zrównoważonym obciążeniem.

1. Ustawianie zmiennych środowiska PowerShell hello

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Utwórz pulę IP frontonu skojarzenie publicznego adresu IP hello utworzone w poprzednim kroku hello i hello modułu równoważenia obciążenia.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Tworzenie hello sondowania, reguł NAT oraz zasady równoważeniem obciążenia

W tym przykładzie jest tworzony hello następujące elementy:

* Sonda toocheck reguły dla łączności tooTCP portu 80
* translator NAT reguły tootranslate cały ruch przychodzący na porcie 3389 tooport 3389 protokołu RDP<sup>1</sup>
* translator NAT reguły tootranslate cały ruch przychodzący na porcie 3391 tooport 3389 protokołu RDP<sup>1</sup>
* toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresów w puli zaplecza hello.

<sup>1</sup> reguł NAT są skojarzone tooa wystąpienia określonej maszyny wirtualnej za hello równoważenia obciążenia. ruch sieciowy Hello przychodzące do portu 3389 jest wysyłane toohello określonej maszyny wirtualnej i skojarzonych z hello reguły NAT portu. Musisz określić protokół (UDP lub TCP) dla reguły NAT. Oba protokoły nie może być przypisana toohello tego samego portu.

1. Ustawianie zmiennych środowiska PowerShell hello

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Utworzyć hello sondy

    Witaj poniższy przykład tworzy sondowaniem TCP sprawdzającą dla łączności tooback-end-port TCP 80 co 15 s. Go spowoduje oznaczenie zasobów zaplecza hello niedostępne po dwóch kolejnych błędów.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Tworzenie reguł ruchu przychodzącego translatora adresów Sieciowych, które połączeń protokołu RDP toohello zaplecza zasobów

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Tworzenie reguł, które przesyłają toodifferent wewnętrznych portów w zależności od tego, które frontonu odebrał żądanie hello modułu równoważenia obciążenia

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Sprawdź ustawienia

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Oczekiwane dane wyjściowe:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>Tworzenie kart sieciowych

Tworzenie kart sieciowych i skojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sondy.

1. Ustawianie zmiennych środowiska PowerShell hello

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Utwórz kartę Sieciową dla każdej zaplecza, a następnie dodaj konfiguracji protokołu IPv6.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Utwórz zasobów maszyny Wirtualnej hello zaplecza i Dołącz poszczególne karty Sieciowe

toocreate maszyn wirtualnych, musisz mieć konto magazynu. W przypadku równoważenia obciążenia hello maszyny wirtualne muszą toobe członkami zestawu dostępności. Aby uzyskać więcej informacji na temat tworzenia maszyn wirtualnych, zobacz [tworzenia maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Ustawianie zmiennych środowiska PowerShell hello

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > W tym przykładzie używane hello nazwy użytkownika i hasła dla maszyn wirtualnych hello w postaci zwykłego tekstu. Odpowiednie należy uważać podczas przy użyciu poświadczeń w hello Wyczyść. Aby bardziej bezpieczne metody obsługi poświadczenia w programie PowerShell, zobacz hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.

2. Tworzenie zestawu dostępności i konto magazynu hello

    Po utworzeniu hello maszyn wirtualnych, może używać istniejącego konta magazynu. Witaj następujące polecenie tworzy nowe konto magazynu.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Następnie należy utworzyć hello zestawu dostępności.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Tworzenie maszyn wirtualnych hello z kartami sieciowymi hello skojarzone

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
