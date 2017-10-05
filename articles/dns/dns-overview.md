---
title: "Omówienie usługi Azure DNS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="589be-104">Omówienie usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="589be-104">Azure DNS overview</span></span>

<span data-ttu-id="589be-105">System nazw domen lub DNS, jest odpowiedzialny za tłumaczenia (lub rozpoznawania) nazwę witryny sieci Web lub usługi na adres IP.</span><span class="sxs-lookup"><span data-stu-id="589be-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="589be-106">Usługa DNS platformy Azure to Usługa hostingu domen DNS, rozpoznawania nazw przy użyciu infrastruktury Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="589be-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="589be-107">Dzięki hostowaniu swoich domen na platformie Azure możesz zarządzać rekordami DNS z zastosowaniem tych samych poświadczeń, interfejsów API, narzędzi i rozliczeń co w przypadku innych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="589be-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Omówienie systemu DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="589be-109">Funkcje</span><span class="sxs-lookup"><span data-stu-id="589be-109">Features</span></span>

* <span data-ttu-id="589be-110">**Niezawodność i wydajność** -domen DNS w usłudze Azure DNS są hostowane w globalnej sieci platformy Azure serwerów nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="589be-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="589be-111">Używamy emisji dowolnej sieci, dzięki czemu każdy zapytanie DNS zostanie odebrane przez najbliższy dostępny serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="589be-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="589be-112">Zapewnia to zarówno duża wydajność i wysoka dostępność dla domeny.</span><span class="sxs-lookup"><span data-stu-id="589be-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="589be-113">**Integracja** — usługa Azure DNS może służyć do zarządzania rekordami DNS dla usług Azure i może służyć do zapewnienia DNS sieci zewnętrznych zasobów.</span><span class="sxs-lookup"><span data-stu-id="589be-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="589be-114">Usługa Azure DNS jest zintegrowana w portalu Azure i używa tych samych poświadczeń, rozliczeń i pomocy technicznej jako innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="589be-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="589be-115">**Zabezpieczenia** — usługa Azure DNS jest oparta na usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="589be-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="589be-116">W efekcie korzysta z funkcji Menedżera zasobów, takich jak kontrola dostępu oparta na rolach, dzienniki inspekcji i blokowanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="589be-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="589be-117">Twoje domenach i rekordach mogą być zarządzane za pośrednictwem portalu Azure, poleceń cmdlet programu PowerShell Azure i wiersza polecenia platformy Azure i platform.</span><span class="sxs-lookup"><span data-stu-id="589be-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="589be-118">Aplikacje wymagające automatycznego zarządzania DNS można zintegrować z usługą za pośrednictwem interfejsu API REST i zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="589be-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="589be-119">Usługa Azure DNS nie obsługuje obecnie zakupów nazw domen.</span><span class="sxs-lookup"><span data-stu-id="589be-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="589be-120">Jeśli chcesz kupić domen, należy użyć Rejestratora nazw domen innych firm.</span><span class="sxs-lookup"><span data-stu-id="589be-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="589be-121">Zazwyczaj rejestratora pobiera małych opłata.</span><span class="sxs-lookup"><span data-stu-id="589be-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="589be-122">Następnie domeny może być hostowana w usłudze Azure DNS zarządzania rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="589be-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="589be-123">Zobacz [Delegowanie domeny do usługi Azure DNS](dns-domain-delegation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="589be-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="589be-124">Cennik</span><span class="sxs-lookup"><span data-stu-id="589be-124">Pricing</span></span>

<span data-ttu-id="589be-125">Karta DNS opiera się na liczbę stref DNS udostępnianych na platformie Azure i liczby zapytań DNS.</span><span class="sxs-lookup"><span data-stu-id="589be-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="589be-126">Aby dowiedzieć się więcej na temat cen, odwiedź stronę [cennik usługi Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="589be-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="589be-127">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="589be-127">FAQ</span></span>

<span data-ttu-id="589be-128">Często zadawane pytania dotyczące usługi Azure DNS, zobacz [DNS platformy Azure — często zadawane pytania](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="589be-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="589be-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="589be-129">Next steps</span></span>

<span data-ttu-id="589be-130">Więcej informacji na temat stref DNS i rekordy odwiedzając: [DNS strefy i rejestruje omówienie](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="589be-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="589be-131">Dowiedz się, jak [utworzyć strefę DNS](./dns-getstarted-create-dnszone-portal.md) w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="589be-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="589be-132">Poznaj inne kluczowe [możliwości sieciowe](../networking/networking-overview.md) platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="589be-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

