---
title: aaaSpecifying ustawienia DNS w pliku konfiguracji sieci wirtualnej | Dokumentacja firmy Microsoft
description: "Jak toochange ustawienia serwera DNS w sieci wirtualnej przy użyciu konfiguracji sieci wirtualnej dla plików w hello klasycznego modelu wdrażania"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Określanie ustawień DNS w pliku konfiguracji sieci wirtualnej
Plik konfiguracji sieci ma dwa elementy, czy można użyć ustawień systemu nazw domen (DNS, Domain Name System) toospecify: **DnsServers** i **DnsServerRef**. Można dodać listę serwerów DNS, określając ich adresy IP i referencyjne toohello nazwy **DnsServers** elementu. Następnie można użyć **DnsServerRef** toospecify element, który wpisów serwera DNS z elementu DnsServers hello są używane do witryny innej sieci w sieci wirtualnej.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono hello klasycznego modelu wdrażania.

plik konfiguracji sieci Hello może zawierać hello następujące elementy. Tytuł Hello każdego elementu jest połączony tooa strona, która udostępnia dodatkowe informacje o elemencie hello ustawienia wartości.

> [!IMPORTANT]
> Aby uzyskać informacje o sposobie tooconfigure hello pliku konfiguracji sieci, zobacz [konfigurowania wirtualnego za pomocą sieci pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md). Informacje o każdym elemencie zawarte w pliku konfiguracji sieci hello, zobacz [schemat konfiguracji sieci wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[DNS Element](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Witaj **nazwa** atrybutu w hello **serwer DNS** element jest używany tylko jako odwołanie dla hello **DnsServerRef** elementu. Reprezentuje nazwę hosta hello powitania serwera DNS. Każdy **serwer DNS** wartość atrybutu musi być unikatowa w hello całej subskrypcji Microsoft Azure
> 
> 

[Element Lokacje sieci wirtualnej](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> W celu toospecify to ustawienie dla elementu witryn sieci wirtualnych hello, musi być wcześniej zdefiniowany w elemencie DNS hello. Witaj DnsServerRef *nazwa* w hello witryn sieci wirtualnych element musi odwoływać się tooa nazwa wybrana w elemencie DNS hello serwer DNS *nazwa*.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Zrozumienie hello [schemat konfiguracji sieci wirtualnych Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Zrozumienie hello [schemat konfiguracji usługi Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Skonfiguruj sieć wirtualną przy użyciu plików konfiguracji sieci](virtual-networks-using-network-configuration-file.md).

