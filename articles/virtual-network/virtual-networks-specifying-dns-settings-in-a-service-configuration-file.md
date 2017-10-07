---
title: "Ustawienia systemu DNS w pliku konfiguracji usługi aaaSpecifying | Dokumentacja firmy Microsoft"
description: "Określanie niestandardowych ustawień DNS dla sieci wirtualnej przy użyciu pliku konfiguracji usługi"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Określanie ustawień DNS w pliku konfiguracji usługi
## <a name="dns-elements"></a>Elementy DNS
Plik konfiguracji usługi może zawierać elementu DnsServers z listy adresów IPv4 dla serwerów systemu nazw domen (DNS, Domain Name System) hello, które będzie używane przez usługę hello. Ustawienia w pliku konfiguracji usługi hello mają pierwszeństwo przed ustawień w pliku konfiguracji sieci hello. Aby uzyskać więcej informacji, zobacz [schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Element Konfiguracja sieci**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Witaj **nazwa** atrybutu w hello **serwer DNS** element jest używany tylko jako nazwy odwołania. Reprezentuje nazwę hosta hello powitania serwera DNS. Każdy **serwer DNS** wartość atrybutu musi być unikatowa w hello całej subskrypcji Microsoft Azure.
> 
> 

## <a name="see-also"></a>Zobacz też
[Schemat konfiguracji usługi Azure (cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Schemat konfiguracji sieci wirtualnej platformy Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Skonfiguruj sieć wirtualną przy użyciu plików konfiguracji sieci](http://go.microsoft.com/fwlink/?LinkId=248094)

[Ustawienia sieci wirtualnej w portalu zarządzania hello — informacje](http://go.microsoft.com/fwlink/?LinkId=248092)

