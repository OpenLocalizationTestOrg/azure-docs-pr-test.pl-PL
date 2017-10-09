---
title: "aaaAutomate NSG inspekcji z widokiem grupy zabezpieczeń obserwatora sieci Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące inspekcji tooconfigure grupy zabezpieczeń sieci"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Automatyzowanie NSG inspekcji z widokiem grupy zabezpieczeń obserwatora sieci platformy Azure

Klienci często występują wyzwanie hello kontrolować stan zabezpieczeń hello infrastruktury. Nie różni się ich maszyn wirtualnych na platformie Azure się tego żądania. Jest ważne toohave podobnego profilu zabezpieczeń oparte na regułach grupy zabezpieczeń sieci (NSG) hello zastosowane. Przy użyciu hello widok grupy zabezpieczeń, można teraz uzyskać hello listę reguł stosowanych tooa maszyny Wirtualnej w ramach grupy NSG. Można zdefiniować złotego profil zabezpieczeń NSG i zainicjować widok grupy zabezpieczeń w okresach co tydzień i porównać profilu toohello złotego wyjściowych hello i utworzyć raport. W ten sposób można zidentyfikować z łatwością wszystkich maszyn wirtualnych hello niezgodnych toohello określony profil zabezpieczeń.

Jeśli nie znasz z grup zabezpieczeń sieci, odwiedź stronę [Przegląd zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu można porównywać grupę zabezpieczeń toohello znanej dobrej linii bazowej wyświetlić wyniki zwracane dla maszyny wirtualnej.

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule pobiera hello widok grupy zabezpieczeń dla maszyny wirtualnej.

W tym scenariuszu obejmują:

- Pobierz zestaw znanych rozsądną regułą
- Pobieranie maszyny wirtualnej z interfejsu API Rest
- Pobierz widok grupy zabezpieczeń dla maszyny wirtualnej
- Ocena odpowiedzi

## <a name="retrieve-rule-set"></a>Pobieranie zestawu reguł

pierwszym krokiem Hello w tym przykładzie jest toowork z istniejącej linii bazowej. Witaj poniższym przykładzie jest niektórych json wyodrębniony z istniejącej grupy zabezpieczeń sieci przy użyciu hello `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet, który jest używany jako jej linia bazowa hello w tym przykładzie.

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a>Konwertowanie obiektów tooPowerShell zestawu reguł

W tym kroku są możemy odczytu pliku json, który został utworzony wcześniej przy użyciu reguł hello, które są oczekiwane toobe na powitania sieciowej grupy zabezpieczeń w tym przykładzie.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Pobrać obserwatora sieciowego

Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia. Witaj `$networkWatcher` zmienna jest przekazywana toohello `AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Uzyskiwanie maszyny Wirtualnej

Maszyna wirtualna jest wymagana toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet przed. Poniższy przykład Hello pobiera obiekt maszyny Wirtualnej.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Pobierz widok grupy zabezpieczeń

Witaj następnym krokiem jest wynik widoku tooretrieve hello zabezpieczeń grupy. Ten wynik jest porównywany toohello "baseline" json, która została przedstawiona wcześniej.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Analizowanie wyników hello

odpowiedź Hello są grupowane według interfejsów sieciowych. Hello różnych typów reguł zwracane są skuteczne i domyślne reguły zabezpieczeń. wynik Hello jest dalsze wyszczególnieniem sposób stosowania, podsieć lub wirtualnych kart sieciowych.

Witaj następujący skrypt programu PowerShell porównuje wyniki hello hello widok grupy zabezpieczeń tooan istniejące dane wyjściowe grupy NSG. Witaj poniższym przykładzie jest prosty przykład sposobu hello wyników może zostać porównane z `Compare-Object` polecenia cmdlet.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Poniższy przykład Hello jest wynikiem hello. Można zauważyć, że dwa hello reguł, które znajdowały się w pierwszym zestawie reguł hello nie były widoczne w porównaniu hello.

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a>Następne kroki

Jeśli ustawienia zostały zmienione, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń znajdujących się w danym.













