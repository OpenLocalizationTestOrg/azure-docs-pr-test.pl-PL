---
title: "aaaOverview usługi Azure DNS | Dokumentacja firmy Microsoft"
description: "Omówienie systemu DNS obsługującego usługę w systemie Microsoft Azure. Hosta domeny w systemie Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="31fd0-104">Omówienie usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="31fd0-104">Azure DNS overview</span></span>

<span data-ttu-id="31fd0-105">System nazw domen Hello lub DNS, jest odpowiedzialny za tłumaczenia (lub rozpoznawania) nazwa witryny sieci Web lub usługi tooits adresu IP.</span><span class="sxs-lookup"><span data-stu-id="31fd0-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="31fd0-106">Usługa DNS platformy Azure to Usługa hostingu domen DNS, rozpoznawania nazw przy użyciu infrastruktury Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="31fd0-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="31fd0-107">Hosting domeny na platformie Azure, można zarządzać systemie DNS rekordów przy użyciu hello tego samego poświadczeń, interfejsy API, narzędzia i rozliczeń jak innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="31fd0-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Omówienie systemu DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="31fd0-109">Funkcje</span><span class="sxs-lookup"><span data-stu-id="31fd0-109">Features</span></span>

* <span data-ttu-id="31fd0-110">**Niezawodność i wydajność** -domen DNS w usłudze Azure DNS są hostowane w globalnej sieci platformy Azure serwerów nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="31fd0-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="31fd0-111">Używamy emisji dowolnej sieci tak, aby każdej zapytanie DNS zostanie odebrane przez serwer DNS dostępne najbliższego hello.</span><span class="sxs-lookup"><span data-stu-id="31fd0-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="31fd0-112">Zapewnia to zarówno duża wydajność i wysoka dostępność dla domeny.</span><span class="sxs-lookup"><span data-stu-id="31fd0-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="31fd0-113">**Integracja** — usługa Azure DNS hello mogą być używane toomanage rekordy DNS dla usługi Azure i mogą być używane tooprovide DNS sieci zewnętrznych zasobów.</span><span class="sxs-lookup"><span data-stu-id="31fd0-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="31fd0-114">Usługa Azure DNS jest zintegrowany z hello portalu Azure i używa hello tych samych poświadczeń, rozliczeń i pomocy technicznej, jak innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="31fd0-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="31fd0-115">**Zabezpieczenia** -hello usługa Azure DNS jest oparta na usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31fd0-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="31fd0-116">W efekcie korzysta z funkcji Menedżera zasobów, takich jak kontrola dostępu oparta na rolach, dzienniki inspekcji i blokowanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="31fd0-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="31fd0-117">Twoje domenach i rekordach mogą być zarządzane za pośrednictwem hello portalu Azure, poleceń cmdlet programu Azure PowerShell, a hello wiersza polecenia platformy Azure i platform.</span><span class="sxs-lookup"><span data-stu-id="31fd0-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="31fd0-118">Aplikacje wymagające automatycznego zarządzania DNS można zintegrować z usługą hello za pośrednictwem hello interfejsu API REST i zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="31fd0-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="31fd0-119">Usługa Azure DNS nie obsługuje obecnie zakupów nazw domen.</span><span class="sxs-lookup"><span data-stu-id="31fd0-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="31fd0-120">Jeśli chcesz toopurchase domen, należy toouse rejestratora nazw domen innych firm.</span><span class="sxs-lookup"><span data-stu-id="31fd0-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="31fd0-121">Rejestrator Hello zazwyczaj pobiera małych opłata.</span><span class="sxs-lookup"><span data-stu-id="31fd0-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="31fd0-122">następnie Hello domeny może być hostowana w usłudze Azure DNS zarządzania rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="31fd0-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="31fd0-123">Zobacz [delegować tooAzure domeny DNS](dns-domain-delegation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="31fd0-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="31fd0-124">Cennik</span><span class="sxs-lookup"><span data-stu-id="31fd0-124">Pricing</span></span>

<span data-ttu-id="31fd0-125">Rozliczeń DNS jest oparta na powitania liczbę stref DNS udostępnianych na platformie Azure i hello liczby zapytań DNS.</span><span class="sxs-lookup"><span data-stu-id="31fd0-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="31fd0-126">więcej informacji na temat cen, odwiedź stronę toolearn [cennik usługi Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="31fd0-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="31fd0-127">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="31fd0-127">FAQ</span></span>

<span data-ttu-id="31fd0-128">Często zadawane pytania dotyczące usługi Azure DNS, zobacz hello [DNS platformy Azure — często zadawane pytania](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="31fd0-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31fd0-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31fd0-129">Next steps</span></span>

<span data-ttu-id="31fd0-130">Więcej informacji na temat stref DNS i rekordy odwiedzając: [DNS strefy i rejestruje omówienie](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="31fd0-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="31fd0-131">Dowiedz się, jak za[utworzyć strefę DNS](./dns-getstarted-create-dnszone-portal.md) w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="31fd0-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="31fd0-132">Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="31fd0-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

