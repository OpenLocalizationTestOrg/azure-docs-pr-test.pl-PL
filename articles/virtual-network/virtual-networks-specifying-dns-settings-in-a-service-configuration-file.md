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
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="4123b-103">Określanie ustawień DNS w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="4123b-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="4123b-104">Elementy DNS</span><span class="sxs-lookup"><span data-stu-id="4123b-104">DNS elements</span></span>
<span data-ttu-id="4123b-105">Plik konfiguracji usługi może zawierać elementu DnsServers z listy adresów IPv4 dla serwerów systemu nazw domen (DNS, Domain Name System), które będą korzystać z usługi.</span><span class="sxs-lookup"><span data-stu-id="4123b-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="4123b-106">Ustawienia w pliku konfiguracji usługi pierwszeństwo względem ustawień w pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="4123b-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="4123b-107">Aby uzyskać więcej informacji, zobacz [schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="4123b-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="4123b-108">**Element Konfiguracja sieci**</span><span class="sxs-lookup"><span data-stu-id="4123b-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="4123b-109">**Nazwa** atrybutu w **serwer DNS** element jest używany tylko jako nazwy odwołania.</span><span class="sxs-lookup"><span data-stu-id="4123b-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="4123b-110">Ten element nie reprezentuje nazwę hosta dla serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="4123b-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="4123b-111">Każdy **serwer DNS** wartość atrybutu musi być unikatowy w całej subskrypcji Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4123b-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="4123b-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4123b-112">See Also</span></span>
[<span data-ttu-id="4123b-113">Schemat konfiguracji usługi Azure (cscfg)</span><span class="sxs-lookup"><span data-stu-id="4123b-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="4123b-114">Schemat konfiguracji sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4123b-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="4123b-115">Skonfiguruj sieć wirtualną przy użyciu plików konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="4123b-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="4123b-116">Ustawienia sieci wirtualnej w portalu zarządzania — informacje</span><span class="sxs-lookup"><span data-stu-id="4123b-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

