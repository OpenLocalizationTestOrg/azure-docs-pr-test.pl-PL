---
title: "aaaManage Azure zastrzeżonych adresów IP (klasyczne) - PowerShell | Dokumentacja firmy Microsoft"
description: "Zrozumienie zastrzeżone adresy IP (klasyczne) i w jaki sposób toomanage ich przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Zastrzeżone adresy IP (klasyczne)

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Szablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klasyczny)](virtual-networks-reserved-public-ip.md)

Adresy IP na platformie Azure można podzielić na dwie kategorie: dynamiczne i zastrzeżone. Publiczne adresy IP, zarządzane przez usługę Azure są dynamiczne domyślnie. Czy oznacza, że hello adres IP używany dla określonej chmury usługi (VIP) lub tooaccess maszyny Wirtualnej lub bezpośrednio wystąpienia roli (ILPIP) może zostać zmieniony z tootime czasu, gdy zasoby są zamknięte lub zatrzymana (cofnięciu przydziału).

adresy IP tooprevent zmianę, można zastrzec adres IP. Zastrzeżonych adresów IP może służyć wyłącznie jako adresu VIP, zapewniając tego hello adresu IP dla usługi w chmurze hello pozostaje hello takie same, nawet jeśli zasoby są zamknięte lub zatrzymana (cofnięciu przydziału). Ponadto można przekonwertować istniejące dynamicznych adresów IP używany jako adres IP tooa zarezerwowane wirtualne adresy IP.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak hello tooreserve statyczny publiczny adres IP przy użyciu [modelu wdrażania usługi Resource Manager](virtual-network-ip-addresses-overview-arm.md).

adresy toolearn więcej informacji na temat adresu IP na platformie Azure, przeczytaj hello [adresów IP](virtual-network-ip-addresses-overview-classic.md) artykułu.

## <a name="when-do-i-need-a-reserved-ip"></a>Jeśli potrzebujesz zastrzeżony adres IP?
* **Ma tooensure, który hello IP jest zarezerwowana w ramach subskrypcji**. Jeśli chcesz tooreserve adresu IP, który nie jest zwalniany z subskrypcją w żadnym przypadku należy używać zastrzeżonego publicznego adresu IP.  
* **Ma toostay Twojego adresu IP z usługi w chmurze, nawet w poprzek zatrzymana lub alokację stanu (VM)**. Jeśli chcesz, aby Twoje toobe usługi dostępne za pośrednictwem adresu IP, który nie ulega zmianie, nawet w przypadku maszyn wirtualnych w hello w chmurze usługi są zamknięte lub Zatrzymaj (cofnięciu przydziału).
* **Ma tooensure, że ruch wychodzący z platformy Azure używa przewidywalną adresu IP**. Może być lokalnymi skonfigurowano zaporę tooallow tylko ruchu z określonych adresów IP. Przez zarezerwowanie adresów IP, wiesz hello źródłowy adres IP adresów i nie trzeba tooupdate reguły zapory powodu tooan zmiany adresów IP.

## <a name="faq"></a>Często zadawane pytania
1. Dla wszystkich usług platformy Azure można używać zastrzeżonego adresu IP? <br>
    Nie. Zastrzeżonych adresów IP można używać tylko dla maszyn wirtualnych i role wystąpienia usługi w chmurze za pośrednictwem adresu VIP.
2. Jak wiele zastrzeżonych adresów IP może mieć? <br>
    Aby uzyskać więcej informacji, zobacz hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.
3. Dla zarezerwowanych adresów IP jest opłatę? <br>
    Czasami. Aby uzyskać szczegółowe informacje o cenach, zobacz hello [zastrzeżonego adresu IP Address szczegóły cennika](http://go.microsoft.com/fwlink/?LinkID=398482) strony.
4. Jak zastrzeżenia adresu IP? <br>
    Korzystając z programu PowerShell, hello [interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), lub hello [portalu Azure](https://portal.azure.com) tooreserve adresu IP w regionie platformy Azure. Zastrzeżony adres IP jest skojarzony tooyour subskrypcji.
5. Czy można używać zastrzeżonego adresu IP z sieci oparte na grupach koligacji wirtualnych? <br>
    Nie. Zastrzeżonych adresów IP są obsługiwane tylko w regionalnych sieci wirtualnych. Zastrzeżonych adresów IP nie są obsługiwane dla sieci wirtualnych, które są skojarzone z grup koligacji. Aby uzyskać więcej informacji o sposobie kojarzenia sieci wirtualnej z region lub grupę koligacji, zobacz hello [o sieci regionalnych wirtualnych i grup koligacji](virtual-networks-migrate-to-regional-vnet.md) artykułu.

## <a name="manage-reserved-vips"></a>Zarządzanie zarezerwowanych adresów VIP

Upewnij się, zostanie zainstalowany i skonfigurowany programu PowerShell, wykonując kroki hello hello [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview) artykułu. 

Przed użyciem zastrzeżonych adresów IP, należy dodać tooyour subskrypcji. toocreate zastrzeżony adres IP z puli hello publicznego adresu IP, adresy dostępne w hello *środkowe stany USA* lokalizacji, uruchom następujące polecenie hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Zwróć uwagę, że nie można określić adresu IP, jakie są zastrzeżone. tooview adresów IP, które są zarezerwowane w ramach subskrypcji, uruchom następujące polecenia programu PowerShell hello i zwróć uwagę, wartości hello *nazwa zastrzeżonego adresu IP* i *adres*:

```powershell
Get-AzureReservedIP
```

Oczekiwane dane wyjściowe:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>Po utworzeniu zastrzeżonego adresu IP przy użyciu programu PowerShell nie można określić IP hello zarezerwowanych zasobów grupy toocreate w. Azure miejsca go do grupy zasobów o nazwie *sieci domyślne* automatycznie. Jeśli utworzysz hello zastrzeżone IP przy użyciu hello [portalu Azure](http://portal.azure.com), można określić dowolną grupę zasobów, możesz wybrać. Jeśli utworzysz IP hello zarezerwowane w grupie zasobów innych niż *sieci domyślne* jednak zawsze, gdy odwołanie hello zastrzeżony adres IP za pomocą polecenia takie jak `Get-AzureReservedIP` i `Remove-AzureReservedIP`, musi odwoływać się nazwy hello *Zarezerwowana nazwa grupy zasobów ip — Nazwa grupy*.  Na przykład w przypadku utworzenia zastrzeżony adres IP o nazwie *myReservedIP* w grupie zasobów o nazwie *myResourceGroup*, musi odwoływać się nazwy hello IP hello zarezerwowane jako *myResourceGroup grupy myReservedIP*.   

Gdy adres IP jest zarezerwowany, pozostaje subskrypcji skojarzone tooyour dopóki nie zostaną usunięte. toodelete zastrzeżonego adresu IP hello uruchom następujące polecenia programu PowerShell:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Zarezerwowania adresu IP hello istniejącą usługę w chmurze
Można zastrzec adresu IP hello istniejącej usługi w chmurze, dodając hello `-ServiceName` parametru. adres IP hello tooreserve usługi w chmurze *TestService* w hello *środkowe stany USA* lokalizacji, uruchom następujące polecenia programu PowerShell hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Skojarzyć zastrzeżonego adresu IP tooa nową usługę w chmurze
Witaj poniższy skrypt tworzy nowy zastrzeżony adres IP, a następnie kojarzy ją tooa nową usługę w chmurze o nazwie *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Po utworzeniu zastrzeżone toouse IP z usługi w chmurze, nadal odwołanie toohello maszyny Wirtualnej za pomocą *VIP:&lt;numer portu >* dla komunikacji przychodzącej. Rezerwacja adresu IP oznacza to, że można połączyć bezpośrednio toohello maszyny Wirtualnej. Witaj zastrzeżony adres IP jest przypisywany toohello chmury usługi hello, że maszyna wirtualna została wdrożona. Jeśli chcesz tooa tooconnect maszynę Wirtualną za IP bezpośrednio, masz tooconfigure publicznego adresu IP poziomie wystąpienia. Publiczny adres IP poziomie wystąpienia jest typu publicznego adresu IP (nazywane ILPIP) przypisane bezpośrednio tooyour maszyny Wirtualnej. Nie można zarezerwować. Aby uzyskać więcej informacji, przeczytaj hello [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) artykułu.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Usuwanie zastrzeżonego adresu IP z wykonywanego wdrożenia
zastrzeżony adres IP tooremove dodane tooa nową usługę w chmurze, uruchom następujące polecenia programu PowerShell hello:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Usuwanie zastrzeżonego adresu IP z wykonywanego wdrożenia nie powoduje usunięcia rezerwacji hello z subskrypcji. Po prostu powoduje zwolnienie hello toobe IP używany przez inny zasób w ramach subskrypcji.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Skojarzyć zastrzeżonego tooa IP uruchamiania wdrożenia
Witaj następujące polecenia tworzenia usługi w chmurze o nazwie *TestService2* z nowej maszyny Wirtualnej o nazwie *TestVM2*. istniejące Hello zastrzeżony adres IP o nazwie *MyReservedIP* jest następnie toohello skojarzona usługa w chmurze.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Skojarzyć zastrzeżonego adresu IP tooa usługą w chmurze przy użyciu pliku konfiguracji usługi
Można również skojarzyć zastrzeżonego adresu IP tooa usługą w chmurze przy użyciu pliku konfiguracji (CSCFG) usługi. Witaj następujące przykładowe xml pokazuje sposób tooconfigure toouse usługi chmury zarezerwowanych adresów VIP o nazwie *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Następne kroki
* Zrozumienie sposobu [adresowanie IP](virtual-network-ip-addresses-overview-classic.md) działa w hello klasycznego modelu wdrażania.
* Dowiedz się więcej o [prywatne adresy IP zarezerwowane](virtual-networks-reserved-private-ip.md).
* Dowiedz się więcej o [adresy IP publicznego poziom wystąpienia (ILPIP)](virtual-networks-instance-level-public-ip.md).

