---
title: "Określanie ustawień DNS w pliku konfiguracji usługi | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Określanie ustawień DNS w pliku konfiguracji usługi
## <a name="dns-elements"></a>Elementy DNS
Plik konfiguracji usługi może zawierać elementu DnsServers z listy adresów IPv4 dla serwerów systemu nazw domen (DNS, Domain Name System), które będą korzystać z usługi. Ustawienia w pliku konfiguracji usługi pierwszeństwo względem ustawień w pliku konfiguracji sieci. Aby uzyskać więcej informacji, zobacz [schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Element Konfiguracja sieci**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> **Nazwa** atrybutu w **serwer DNS** element jest używany tylko jako nazwy odwołania. Ten element nie reprezentuje nazwę hosta dla serwera DNS. Każdy **serwer DNS** wartość atrybutu musi być unikatowy w całej subskrypcji Microsoft Azure.
> 
> 

## <a name="see-also"></a>Zobacz też
[Schemat konfiguracji usługi Azure (cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Schemat konfiguracji sieci wirtualnej platformy Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Skonfiguruj sieć wirtualną przy użyciu plików konfiguracji sieci](http://go.microsoft.com/fwlink/?LinkId=248094)

[Ustawienia sieci wirtualnej w portalu zarządzania — informacje](http://go.microsoft.com/fwlink/?LinkId=248092)

