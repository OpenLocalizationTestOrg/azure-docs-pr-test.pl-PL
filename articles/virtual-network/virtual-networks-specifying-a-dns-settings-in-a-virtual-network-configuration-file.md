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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="1c3b4-103">Określanie ustawień DNS w pliku konfiguracji sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1c3b4-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="1c3b4-104">Plik konfiguracji sieci ma dwa elementy, czy można użyć ustawień systemu nazw domen (DNS, Domain Name System) toospecify: **DnsServers** i **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="1c3b4-105">Można dodać listę serwerów DNS, określając ich adresy IP i referencyjne toohello nazwy **DnsServers** elementu.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="1c3b4-106">Następnie można użyć **DnsServerRef** toospecify element, który wpisów serwera DNS z elementu DnsServers hello są używane do witryny innej sieci w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1c3b4-107">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="1c3b4-108">plik konfiguracji sieci Hello może zawierać hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="1c3b4-109">Tytuł Hello każdego elementu jest połączony tooa strona, która udostępnia dodatkowe informacje o elemencie hello ustawienia wartości.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3b4-110">Aby uzyskać informacje o sposobie tooconfigure hello pliku konfiguracji sieci, zobacz [konfigurowania wirtualnego za pomocą sieci pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b4-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="1c3b4-111">Informacje o każdym elemencie zawarte w pliku konfiguracji sieci hello, zobacz [schemat konfiguracji sieci wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c3b4-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="1c3b4-112">DNS Element</span><span class="sxs-lookup"><span data-stu-id="1c3b4-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="1c3b4-113">Witaj **nazwa** atrybutu w hello **serwer DNS** element jest używany tylko jako odwołanie dla hello **DnsServerRef** elementu.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="1c3b4-114">Reprezentuje nazwę hosta hello powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="1c3b4-115">Każdy **serwer DNS** wartość atrybutu musi być unikatowa w hello całej subskrypcji Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1c3b4-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="1c3b4-116">Element Lokacje sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1c3b4-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="1c3b4-117">W celu toospecify to ustawienie dla elementu witryn sieci wirtualnych hello, musi być wcześniej zdefiniowany w elemencie DNS hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="1c3b4-118">Witaj DnsServerRef *nazwa* w hello witryn sieci wirtualnych element musi odwoływać się tooa nazwa wybrana w elemencie DNS hello serwer DNS *nazwa*.</span><span class="sxs-lookup"><span data-stu-id="1c3b4-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1c3b4-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c3b4-119">Next steps</span></span>
* <span data-ttu-id="1c3b4-120">Zrozumienie hello [schemat konfiguracji sieci wirtualnych Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="1c3b4-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="1c3b4-121">Zrozumienie hello [schemat konfiguracji usługi Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="1c3b4-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="1c3b4-122">[Skonfiguruj sieć wirtualną przy użyciu plików konfiguracji sieci](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b4-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

