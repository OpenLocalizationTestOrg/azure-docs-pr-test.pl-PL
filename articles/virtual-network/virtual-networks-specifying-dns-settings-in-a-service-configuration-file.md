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
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="cc5f8-103">Określanie ustawień DNS w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="cc5f8-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="cc5f8-104">Elementy DNS</span><span class="sxs-lookup"><span data-stu-id="cc5f8-104">DNS elements</span></span>
<span data-ttu-id="cc5f8-105">Plik konfiguracji usługi może zawierać elementu DnsServers z listy adresów IPv4 dla serwerów systemu nazw domen (DNS, Domain Name System) hello, które będzie używane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f8-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="cc5f8-106">Ustawienia w pliku konfiguracji usługi hello mają pierwszeństwo przed ustawień w pliku konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f8-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="cc5f8-107">Aby uzyskać więcej informacji, zobacz [schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc5f8-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="cc5f8-108">**Element Konfiguracja sieci**</span><span class="sxs-lookup"><span data-stu-id="cc5f8-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="cc5f8-109">Witaj **nazwa** atrybutu w hello **serwer DNS** element jest używany tylko jako nazwy odwołania.</span><span class="sxs-lookup"><span data-stu-id="cc5f8-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="cc5f8-110">Reprezentuje nazwę hosta hello powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="cc5f8-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="cc5f8-111">Każdy **serwer DNS** wartość atrybutu musi być unikatowa w hello całej subskrypcji Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc5f8-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="cc5f8-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cc5f8-112">See Also</span></span>
[<span data-ttu-id="cc5f8-113">Schemat konfiguracji usługi Azure (cscfg)</span><span class="sxs-lookup"><span data-stu-id="cc5f8-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="cc5f8-114">Schemat konfiguracji sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc5f8-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="cc5f8-115">Skonfiguruj sieć wirtualną przy użyciu plików konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="cc5f8-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="cc5f8-116">Ustawienia sieci wirtualnej w portalu zarządzania hello — informacje</span><span class="sxs-lookup"><span data-stu-id="cc5f8-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

