---
title: "aaaStatic wewnętrzny prywatnej Classic IP - Azure VM -"
description: "Opis statyczne wewnętrzne adresy IP (DIP) i w jaki sposób toomanage ich"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Jak tooset wewnętrzny statycznego prywatnego adresu IP adresów przy użyciu programu PowerShell (klasyczne)
W większości przypadków nie ma potrzeby toospecify wewnętrzny statyczny adres IP dla maszyny wirtualnej. Maszyn wirtualnych w sieci wirtualnej zostanie automatycznie otrzymują wewnętrzny adres IP z zakresu, który określisz. Jednak w niektórych przypadkach Określanie statycznego adresu IP dla określonej maszyny Wirtualnej ma sens. Na przykład, jeśli maszyna wirtualna będzie toorun DNS jest lub będzie kontroler domeny. Statyczny adres IP wewnętrznego utrzymane hello maszyny Wirtualnej, nawet za pośrednictwem stanu zatrzymania/deprovision. 

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca się, że większości nowych wdrożeń korzystać hello [modelu wdrażania usługi Resource Manager](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Jak tooverify, jeśli określony adres IP jest dostępna
tooverify Jeśli hello adres IP *10.0.0.7* jest dostępny w sieci wirtualnej o nazwie *TestVnet*, uruchom następujące polecenia programu PowerShell hello i sprawdź wartość hello *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Polecenie hello tootest powyżej w bezpiecznym środowisku należy wykonać wytyczne hello w [utworzyć sieć wirtualną (klasyczne)](virtual-networks-create-vnet-classic-pportal.md) toocreate sieć wirtualną o nazwie *TestVnet* i upewnij się, używa hello  *10.0.0.0/8* przestrzeni adresów.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Jak toospecify statycznego wewnętrznego adresu IP podczas tworzenia maszyny Wirtualnej
Poniższy skrypt programu PowerShell Hello tworzy nową usługę w chmurze o nazwie *TestService*, pobiera obraz z platformy Azure, a następnie tworzy Maszynę wirtualną o nazwie *TestVM* hello nowego w usłudze w chmurze przy użyciu obrazu hello pobrać Ustawia hello toobe maszyn wirtualnych w podsieci o nazwie *podsieć 1*i ustawia *10.0.0.7* jako statyczny adres IP wewnętrznego dla hello maszyny Wirtualnej:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Jak tooretrieve statyczne wewnętrzne informacje o adresie IP dla maszyny Wirtualnej
tooview hello wewnętrznego adresu IP informacje dotyczące statycznych hello maszyny Wirtualnej utworzone za pomocą skryptu hello powyżej, uruchom następujące polecenia programu PowerShell hello i sprawdź wartości hello *IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Jak tooremove statyczny adres IP wewnętrznego z maszyny Wirtualnej
tooremove hello statycznego wewnętrznego adresu IP dodane toohello maszyny Wirtualnej w skrypcie hello powyżej, uruchom hello następującego polecenia programu PowerShell:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Jak tooadd statyczne wewnętrzne tooan IP istniejącej maszyny Wirtualnej
tooadd statyczne wewnętrzne toohello IP maszyny Wirtualnej utworzonej przy użyciu skryptu hello powyżej runt następujące polecenie:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Następne kroki
[Zastrzeżony adres IP](virtual-networks-reserved-public-ip.md)

[Poziom wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md)

[Interfejsy API REST zastrzeżonego adresu IP](https://msdn.microsoft.com/library/azure/dn722420.aspx)

