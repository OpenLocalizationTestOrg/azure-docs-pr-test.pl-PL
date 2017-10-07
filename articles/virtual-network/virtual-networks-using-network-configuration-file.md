---
title: "aaaConfigure sieci wirtualnej platformy Azure (klasyczne) — plik konfiguracji sieci | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i modyfikowania sieci wirtualnych (klasyczne) przez eksportowanie, zmienianie i importowanie pliku konfiguracji sieci."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Skonfiguruj sieć wirtualną (klasyczne) przy użyciu pliku konfiguracji sieci
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać modelu wdrażania usługi Resource Manager hello.

Można tworzyć i konfigurować sieć wirtualna (klasyczna) z pliku konfiguracji sieci przy użyciu hello Azure interfejsu wiersza polecenia (CLI) 1.0 lub Azure PowerShell. Nie można utworzyć lub zmodyfikować sieć wirtualną przy użyciu modelu wdrażania usługi Azure Resource Manager hello przy użyciu pliku konfiguracji sieci. Nie można użyć hello toocreate portalu Azure lub zmodyfikować sieci wirtualnej (klasyczne) przy użyciu pliku konfiguracji sieci, jednak można korzystać hello toocreate portalu Azure (klasyczną), sieci wirtualnej bez użycia pliku konfiguracji sieci.

Tworzenie i konfigurowanie sieci wirtualnej (klasyczne) przy użyciu pliku konfiguracji sieci wymaga eksportowanie, zmienianie i importowanie pliku hello.

## <a name="export"></a>Eksportowanie plików konfiguracji sieci

Możesz użyć programu PowerShell lub hello Azure CLI tooexport pliku konfiguracji sieci. PowerShell eksportuje pliku XML, gdy hello Azure CLI eksportuje pliku json.

### <a name="powershell"></a>PowerShell
 
1. [Instalowanie programu Azure PowerShell i logowanie tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Zmień katalog hello (i upewnij się, istnieje) i nazwę pliku w hello następujące polecenie jako odpowiednie, a następnie uruchom hello polecenia tooexport hello sieci pliku konfiguracji:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

1. [Zainstaluj hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Wykonaj pozostałe kroki w wierszu polecenia, Azure CLI 1.0 hello.
2. Zaloguj się za tooAzure wprowadzając hello `azure login` polecenia.
3. Upewnij się, jest w trybie asm wprowadzając hello `azure config mode asm` polecenia.
4. Zmień katalog hello (i upewnij się, istnieje) i nazwę pliku w hello następujące polecenie jako odpowiednie, a następnie uruchom hello polecenia tooexport hello sieci pliku konfiguracji:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Utwórz lub zmodyfikuj plik konfiguracji sieci

Plik konfiguracji sieci jest plik XML (w przypadku używania programu PowerShell) lub plik json (w przypadku używania hello Azure CLI). Możesz edytować plik hello w dowolnym tekstu lub edytora XML/json. Witaj [ustawienia schematu pliku konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx) artykuł zawiera szczegółowe informacje o wszystkich ustawieniach. Dodatkowe wyjaśnienie hello ustawień, zobacz [wyświetlić sieci wirtualnych i ustawienia](virtual-network-manage-network.md#view-vnet). Witaj wprowadzone zmiany pliku toohello:

- Musi być zgodne z hello schematu lub importowania sieci hello pliku konfiguracji nie powiedzie się.
- Zastąp wszystkie istniejące ustawienia sieci dla Twojej subskrypcji, dlatego należy zachować wyjątkową ostrożność podczas wprowadzania zmian. Na przykład odwołanie hello przykład sieci pliki konfiguracyjne, które należy wykonać. Powiedz hello oryginalny plik zawiera dwa **VirtualNetworkSite** wystąpienia, a uległ zmianie, jak przedstawiono w przykładach hello. Podczas importowania pliku hello Azure usuwa hello sieć wirtualną hello **VirtualNetworkSite** usunięte w pliku hello wystąpienia. W tym scenariuszu uproszczony przyjęto zostały żadnych zasobów w sieci wirtualnej hello, jak w przypadku, nie można usunąć sieci wirtualnej hello i hello import nie powiedzie się.

> [!IMPORTANT]
> Azure uwzględnia podsieć, która ma coś wdrożone tooit jako **używany**. Gdy używany jest podsieci, nie można modyfikować. Przed zmodyfikowaniem informacji o podsieci w pliku konfiguracji sieci, należy przenieść wszystkie elementy, które zostały wdrożone toohello podsieci tooa innej podsieci, która nie jest modyfikowany. Zobacz [przenoszenia maszyny Wirtualnej lub wystąpienia roli tooa innej podsieci](virtual-networks-move-vm-role-to-subnet.md) szczegółowe informacje.

### <a name="example-xml-for-use-with-powershell"></a>Przykład XML do użycia przy użyciu programu PowerShell

Witaj następujący przykładowy plik konfiguracji sieci tworzy sieć wirtualną o nazwie *myVirtualNetwork* się na przestrzeń adresową z *10.0.0.0/16* w hello *wschodnie stany USA* Azure region. sieć wirtualna Hello zawiera jedną podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Plik konfiguracji sieci hello wyeksportowanymi zawiera zawartość nie, można skopiować hello XML w poprzednim przykładzie hello i wklej go do nowego pliku.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Przykład JSON do użycia z hello Azure CLI w wersji 1.0

Witaj następujący przykładowy plik konfiguracji sieci tworzy sieć wirtualną o nazwie *myVirtualNetwork* się na przestrzeń adresową z *10.0.0.0/16* w hello *wschodnie stany USA* Azure region. sieć wirtualna Hello zawiera jedną podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Plik konfiguracji sieci hello wyeksportowanymi zawiera zawartość nie, można skopiować hello json w poprzednim przykładzie hello i wklej go do nowego pliku.

## <a name="import"></a>Importowanie pliku konfiguracji sieci

Możesz użyć programu PowerShell lub hello Azure CLI tooimport pliku konfiguracji sieci. PowerShell importuje plik XML, gdy hello Azure CLI importuje plik json. Jeśli hello zakończyła się niepowodzeniem, upewnij się, czy plik hello jest zgodny z hello [schemat konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Instalowanie programu Azure PowerShell i logowanie tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Zmień katalog hello i nazwę pliku w hello następujące polecenie, w razie potrzeby, a następnie uruchom plik konfiguracji sieci tooimport hello hello polecenia:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

1. [Zainstaluj hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Wykonaj pozostałe kroki w wierszu polecenia, Azure CLI 1.0 hello.
2. Zaloguj się za tooAzure wprowadzając hello `azure login` polecenia.
3. Upewnij się, jest w trybie asm wprowadzając hello `azure config mode asm` polecenia.
4. Zmień katalog hello i nazwę pliku w hello następujące polecenie, w razie potrzeby, a następnie uruchom plik konfiguracji sieci tooimport hello hello polecenia:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
