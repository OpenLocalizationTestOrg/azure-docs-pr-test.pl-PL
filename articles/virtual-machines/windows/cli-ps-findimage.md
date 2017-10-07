---
title: obrazy aaaSelect maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodetermine programu Azure PowerSHell toouse hello wydawcy, oferty, jednostki SKU i wersji dla obrazów maszyn wirtualnych w witrynie Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Jak obrazy toofind maszyny Wirtualnej systemu Windows w programie hello Azure Marketplace przy użyciu programu Azure PowerShell

W tym temacie opisano, jak obrazy toouse programu Azure PowerShell toofind maszyny Wirtualnej w programie hello Azure Marketplace. Podczas tworzenia maszyny Wirtualnej systemu Windows za pomocą tej informacji toospecify obrazu z witryny Marketplace.

Upewnij się, że zainstalowane i skonfigurowane hello najnowszych [modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tabela często używane obrazów systemu Windows
| PublisherName | Oferta | SKU |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |Centrum danych 2016 |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016 centrum danych z kontenerów |
| MicrosoftWindowsServer |WindowsServer |2016-Nano serwer |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008 R2 SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016 WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2 WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Znajdowanie określonych obrazów


Podczas tworzenia nowej maszyny wirtualnej za pomocą Menedżera zasobów Azure, w niektórych przypadkach należy toospecify obrazu z kombinacją hello hello następujące właściwości obrazu:

* Wydawca
* Oferta
* SKU

Na przykład użyć tych wartości z hello [AzureRMVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage) polecenia cmdlet programu PowerShell lub przy użyciu szablonu grupy zasobów, w którym należy określić typ hello toobe maszyny Wirtualnej utworzone.

Toodetermine tych wartości, należy wykonać hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), i [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) poleceń cmdlet toonavigate hello obrazów. Należy określić te wartości:

1. Lista wydawców obraz powitania.
2. Dla danego wydawcy wyświetl listę ofert.
3. Dla danej oferty wyświetl listę wersji SKU.

Po pierwsze lista wydawców hello z hello następującego polecenia:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Wypełnij nazwę wybranego wydawcy, a następnie uruchom następujące polecenia hello:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Wypełnij nazwę wybranego oferty, a następnie uruchom następujące polecenia hello:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Z danych wyjściowych hello hello `Get-AzureRMVMImageSku` polecenie ma wszystkie informacje hello potrzebne toospecify hello obrazu dla nowej maszyny wirtualnej.

Oto Hello pełny przykład:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Dane wyjściowe:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Dla wydawcy "MicrosoftWindowsServer" hello:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Dane wyjściowe:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Oferta "Windows Server" hello:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Dane wyjściowe:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

Z tej listy, skopiuj hello wybrana nazwa jednostki SKU i mieć wszystkie informacje hello hello `Set-AzureRMVMSourceImage` polecenia cmdlet programu PowerShell lub szablonu grupy zasobów.

## <a name="next-steps"></a>Następne kroki
Teraz można wybrać dokładnie hello obraz ma toouse. Zobacz maszynę wirtualną, używając szybko hello obrazu informacje, które właśnie znaleziony, toocreate [Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell](quick-create-powershell.md).
