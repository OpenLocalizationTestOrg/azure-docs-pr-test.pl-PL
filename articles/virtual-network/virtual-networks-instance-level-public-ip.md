---
title: "aaaAzure poziomie wystąpienia publicznego adresu IP (klasyczne) dotyczy | Dokumentacja firmy Microsoft"
description: "Zrozumienie poziomu publiczne adresy IP (ILPIP) wystąpienia i w jaki sposób toomanage ich przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Wystąpienia publicznego adresu IP (klasyczne) omówienie
Wystąpienie poziomu publicznego adresu IP (ILPIP) to publiczny adres IP, który można przypisać bezpośrednio tooa wystąpienia roli maszyny Wirtualnej lub usługi w chmurze, a nie toohello usługi w chmurze maszyny Wirtualnej lub roli wystąpienia znajdują się w. ILPIP nie została wykonana hello z hello wirtualnego adresu IP (VIP) przypisany tooyour usługi w chmurze. Jest to raczej dodatkowy adres IP służy tooconnect bezpośrednio tooyour maszyny Wirtualnej lub roli wystąpienia.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca tworzenie maszyn wirtualnych za pomocą Menedżera zasobów. Upewnij się, że rozumiesz, jak [adresów IP](virtual-network-ip-addresses-overview-classic.md) pracy na platformie Azure.

![Różnica między ILPIP i adresu VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Jak pokazano na rysunku 1, usługa w chmurze hello jest dostępny przy użyciu adresu VIP, podczas hello poszczególnych maszyn wirtualnych są zwykle dostępne przy użyciu adresu VIP:&lt;numer portu&gt;. Przypisując tooa ILPIP określonej maszyny Wirtualnej, które mogą być maszyny Wirtualnej dostępne bezpośrednio przy użyciu tego adresu IP.

Podczas tworzenia usługi w chmurze na platformie Azure, odpowiednie rekordy A systemu DNS są tworzone automatycznie tooallow dostępu toohello usługi za pośrednictwem pełną nazwę domeny (FQDN), zamiast rzeczywistego adresu VIP hello. Witaj, który sam proces odbywa się w ILPIP, umożliwiając dostęp toohello maszyny Wirtualnej lub roli wystąpienia przez nazwę FQDN zamiast hello ILPIP. Na przykład w przypadku utworzenia usługi w chmurze o nazwie *contosoadservice*, i skonfigurować rolę sieci web o nazwie *contosoweb* z dwoma wystąpieniami hello Azure rejestruje następujące A rekordów dla wystąpień hello:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> Można przypisać tylko jednego ILPIP dla każdego wystąpienia maszyny Wirtualnej lub roli. Może zużywać ILPIPs too5 na subskrypcję. ILPIPs nie są obsługiwane dla maszyn wirtualnych z wieloma kartami Sieciowymi.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Dlaczego może zażądać ILPIP?
Toobe stanie tooconnect tooyour maszyny Wirtualnej lub wystąpienia roli przy użyciu adresu IP bezpośrednio przypisać tooit, zamiast używania hello chmury usługi VIP:&lt;numer portu&gt;, żądania ILPIP dla maszyny Wirtualnej lub wystąpienia roli.

* **Aktywne FTP** -przypisując tooa ILPIP maszyny Wirtualnej, może odbierać ruch na dowolnym porcie. Punkty końcowe nie są wymagane dla hello ruch tooreceive maszyn wirtualnych.  Zobacz (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Omówienie protokołu FTP] szczegółowe informacje na temat protokołu hello FTP.
* **Wychodzącego** — ruch wychodzący z hello maszyna wirtualna jest zamapowany toohello ILPIP jako źródło hello i hello ILPIP unikatowo identyfikuje jednostki tooexternal maszyny Wirtualnej hello.

> [!NOTE]
> W ciągu ostatnich hello adres ILPIP został określony tooas publicznego adresu IP (PIP).
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Zarządzanie ILPIP dla maszyny Wirtualnej
następujące zadania Hello Włącz toocreate, przypisz i Usuń ILPIPs z maszyn wirtualnych:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Jak toorequest ILPIP podczas tworzenia maszyny Wirtualnej przy użyciu programu PowerShell
usługi w chmurze o nazwie tworzy Hello następującego skryptu programu PowerShell *FTPService*, pobiera obraz z platformy Azure, tworzy Maszynę wirtualną o nazwie *FTPInstance* przy użyciu obrazu hello pobrać ustawia hello wirtualna toouse ILPIP i dodaje hello wirtualna toohello nowej usługi:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Jak tooretrieve ILPIP informacji dla maszyny Wirtualnej
hello tooview informacji ILPIP dla hello maszyny Wirtualnej utworzone za pomocą skryptu poprzedniej hello, uruchom następujące polecenia programu PowerShell hello i obserwować wartości hello *PublicIPAddress* i *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Oczekiwane dane wyjściowe:
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Jak tooremove ILPIP z maszyny Wirtualnej
w poprzedniej skryptu hello, uruchom następujące polecenia programu PowerShell hello tooremove hello ILPIP dodaje toohello maszyny Wirtualnej:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Jak tooadd tooan ILPIP istniejącej maszyny Wirtualnej
tooadd toohello ILPIP maszyny Wirtualnej utworzonej przy użyciu skryptu hello poprzedniego, uruchom następujące polecenie hello:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Zarządzanie ILPIP dla wystąpienia roli usługi w chmurze

tooadd ILPIP tooa usługi w chmurze wystąpienia roli, pełną hello następujące kroki:

1. Pobrać plik .cscfg hello hello usługi w chmurze, wykonując hello etapami hello [jak usług w chmurze tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artykułu.
2. Plik .cscfg hello aktualizacji przez dodanie hello `InstanceAddress` elementu. Witaj następującym przykładowym dodaje ILPIP o nazwie *MyPublicIP* tooa wystąpienia roli o nazwie *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Przesyłanie pliku .cscfg hello hello usługi w chmurze, wykonując hello etapami hello [jak usług w chmurze tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artykułu.

## <a name="next-steps"></a>Następne kroki
* Zrozumienie sposobu [adresowanie IP](virtual-network-ip-addresses-overview-classic.md) działa w hello klasycznego modelu wdrażania.
* Dowiedz się więcej o [zastrzeżone adresy IP](virtual-networks-reserved-public-ip.md).
