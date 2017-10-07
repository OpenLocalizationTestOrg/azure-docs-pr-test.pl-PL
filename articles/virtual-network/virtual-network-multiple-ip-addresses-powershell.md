---
title: "aaaMultiple adresów IP dla maszyn wirtualnych platformy Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP maszyny wirtualnej tooa przy użyciu programu PowerShell | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Przypisz wielu adresów IP maszyny toovirtual przy użyciu programu PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

W tym artykule opisano, jak toocreate maszynę wirtualną (VM) do wdrożenia usługi Azure Resource Manager hello modelu przy użyciu programu PowerShell. Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania. więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP

Hello przestrzeganie objaśniono sposób toocreate przykład maszynę Wirtualną za pomocą wielu IP adresów, zgodnie z opisem w scenariuszu hello. Zmienianie wartości zmiennych, co jest wymagane dla implementacji.

1. Otwórz wiersz polecenia programu PowerShell i pełny hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji programu PowerShell. Jeśli nie masz jeszcze programu PowerShell zainstalowany i skonfigurowany, pełną hello etapami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.
2. Konto logowania tooyour z hello `login-azurermaccount` polecenia.
3. Zastąp *myResourceGroup* i *westus* przy użyciu nazwy i lokalizacji wybrane. Utwórz grupę zasobów. Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Utwórz sieć wirtualną (VNet) i podsieci w hello tej samej lokalizacji co hello grupy zasobów:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Utwórz grupę zabezpieczeń sieci (NSG) i zasady. Witaj NSG zabezpiecza hello maszyny Wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego. W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 3389, która umożliwia nawiązywanie przychodzących połączeń pulpitu zdalnego.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Zdefiniuj hello podstawową konfigurację protokołu IP dla hello karty sieciowej. Zmień 10.0.0.4 tooa prawidłowy adres w podsieci hello zostało utworzone, jeśli nie użyto wartości hello wcześniej zdefiniowane. Przed przypisaniem statycznego adresu IP, zalecane jest, że należy najpierw upewnij się, że nie jest już używana. Wprowadź polecenie hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Jeśli adres hello jest dostępny, hello output zwraca *True*. Jeśli nie jest dostępna, hello output zwraca *False* oraz listę adresów, które są dostępne. 

    W następujące polecenia, hello **Zamień < Zamień z your unikatowy nazwa-> hello unikatowy toouse nazwy DNS.** Nazwa Hello musi być unikatowa we wszystkich publicznych adresów IP w obrębie regionu platformy Azure. Jest to parametr opcjonalny. Można usunąć, jeśli chcesz tylko toohello tooconnect maszyny Wirtualnej przy użyciu hello publicznego adresu IP.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Po przypisaniu wielu tooa konfiguracji adresu IP karty Sieciowej, jednej konfiguracji musi być przypisany jako hello *— podstawowy*.

    > [!NOTE]
    > Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.

7. Zdefiniuj hello dodatkowej konfiguracji adresów IP hello karty sieciowej. Można dodawać i usuwać konfiguracje w razie potrzeby. Każdej konfiguracji adresu IP musi mieć przypisany prywatny adres IP. Każdej konfiguracji opcjonalnie może mieć przypisany jeden publiczny adres IP.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Utworzyć hello kartę Sieciową i skojarzyć hello trzy tooit konfiguracji adresu IP:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Chociaż wszystkie konfiguracje są przypisane tooone karty Sieciowej, w tym artykule, można przypisać toohello kartę Sieciową podłączoną tooevery konfiguracji IP wiele maszyn wirtualnych. jak toocreate Maszynę wirtualną z wieloma kartami sieciowymi, przeczytaj toolearn hello [tworzenia maszyn wirtualnych z wieloma kartami sieciowymi](virtual-network-deploy-multinic-arm-ps.md) artykułu.

9. Utwórz hello maszyny Wirtualnej, wprowadzając hello następującego polecenia:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.

## <a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej

Wykonując kroki hello, które należy wykonać, można dodać prywatnych i publicznych tooa adresy IP karty Sieciowej. Witaj przykłady w hello następujące sekcje założono, że już istnieje Maszynę wirtualną z konfiguracji adresów IP hello trzech opisanych w hello [scenariusza](#Scenario) w tym artykule, ale nie jest to wymagane wykonanie.

1. Otwórz wiersz polecenia programu PowerShell i pełny hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji programu PowerShell. Jeśli nie masz jeszcze programu PowerShell zainstalowany i skonfigurowany, pełną hello etapami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.
2. Zmień hello "wartości" hello nazwę toohello $Variables hello karta sieciowa ma tooadd IP address tooand hello zasobu lokalizacji i grupy powitalne karta sieciowa istnieje w następujących:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Jeśli nie znasz nazwę hello hello ma toochange karty Sieciowej, wprowadź hello następujące polecenia, a następnie zmień hello wartości zmiennych poprzedniej hello:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Utwórz zmienną i ustaw ją toohello istniejących kart interfejsu Sieciowego, wpisując następujące polecenie hello:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. W hello następujące polecenia, zmień *MyVNet* i *MySubnet* toohello nazwy hello sieci wirtualnej i podsieci hello jest połączona karta sieciowa. Wprowadź hello polecenia tooretrieve hello sieci wirtualnej i podsieci obiektów hello podłączenia karty Sieciowej:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Jeśli nie znasz hello sieci wirtualnej lub podsieci nazwę hello podłączenia karty Sieciowej, wprowadź hello następujące polecenie:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    W danych wyjściowych hello Wyszukaj tekst toohello podobne następujące przykładowe dane wyjściowe:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    W tym danych wyjściowych *MyVnet* jest hello sieci wirtualnej i *MySubnet* jest hello podsieci hello jest połączona karta sieciowa.

5. Wykonaj kroki hello w jednym z następujących sekcji, w zależności od wymagań hello:

    **Dodaj prywatnego adresu IP**

    tooadd prywatnej tooa adresu IP karty Sieciowej, należy utworzyć konfigurację protokołu IP. Witaj następujące polecenie tworzy konfiguracji ze statycznym adresem IP 10.0.0.7. Określanie statycznego adresu IP, musi być nieużywany adres podsieci hello. Zaleca się przetestowanie tooensure adres hello jest dostępna, wprowadzając hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` polecenia. Jeśli adres IP hello jest dostępny, hello output zwraca *True*. Jeśli nie jest dostępna, hello output zwraca *False*oraz listę adresów, które są dostępne.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).

    Dodaj hello prywatnego adresu IP adres toohello maszyny Wirtualnej systemu operacyjnego, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.

    **Dodaj publiczny adres IP**

    Publiczny adres IP jest dodawany przez skojarzenie publicznego tooeither zasobów adresu IP nowej konfiguracji IP lub istniejącej konfiguracji adresu IP. Wykonaj kroki hello w jednym z hello kolejnych sekcjach, ile potrzebujesz.

    > [!NOTE]
    > Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.
    >

    - **Skojarz hello publicznej konfiguracji adresu IP zasobu tooa nowego adresu IP**
    
        Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP. Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową. toocreate nową, wprowadź następujące polecenie hello:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        toocreate nowej konfiguracji IP przy użyciu statycznego prywatnego adresu IP i hello skojarzone *myPublicIp3* publicznego adresu IP adresów zasobów, wpisz następujące polecenie hello:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Skojarz hello publicznej konfiguracji adresu IP zasobu tooan istniejącego adresu IP**

        Zasób publicznego adresu IP może być tylko skojarzone tooan konfiguracji adresów IP, który nie ma jeszcze skojarzone. Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie hello:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Zostaną wyświetlone dane wyjściowe podobne toohello poniżej:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Ponieważ hello **publicznego adresu IP** kolumny dla *IpConfig 3* jest puste, zasobu bez publicznego adresu IP jest obecnie skojarzone tooit. Można dodać istniejącego publicznego adresu IP adres zasobów tooIpConfig-3, lub wprowadź powitania po toocreate polecenia, co:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Wprowadź następujące polecenie publicznego adresu IP tooassociate hello adresów zasobów toohello istniejącej konfiguracji IP o nazwie hello *IpConfig 3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Ustaw hello kart przy użyciu nowej konfiguracji IP hello wprowadzając hello następujące polecenie:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Wyświetlanie hello prywatnych adresów IP i hello publicznego adresu IP adres zasobów przypisanych toohello hello karty Sieciowej, wprowadzając następujące polecenie:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Dodaj hello prywatnego adresu IP adres toohello maszyny Wirtualnej systemu operacyjnego, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP address toohello systemu operacyjnego.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
