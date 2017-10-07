---
title: "aaaProtecting Azure SQL service i danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten adres dokumentu zalecenia w Centrum zabezpieczeń Azure, które ułatwiają ochronę danych i usługą SQL platformy Azure i są aktualizowane zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="7f4c2-103">Ochrona usługi Azure SQL i danych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="7f4c2-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="7f4c2-104">Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="7f4c2-105">Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania kontrolek hello potrzebne hello.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="7f4c2-106">Zalecenia dotyczące zastosować tooAzure typy zasobów: maszynach wirtualnych (VM), sieci, SQL i danych i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="7f4c2-107">W tym artykule opisano zalecenia dotyczące usługi SQL tooAzure i danych.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="7f4c2-108">Zalecenia Centrum wokół Włączanie inspekcji baz danych, włączenie szyfrowania dla baz danych i włączenie szyfrowania konta magazynu Azure i serwerów SQL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="7f4c2-109">Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć hello dostępne SQL service i dane zalecenia i jak każdej z nich działa w przypadku zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="7f4c2-110">Dostępne zalecenia usługi i danych SQL</span><span class="sxs-lookup"><span data-stu-id="7f4c2-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="7f4c2-111">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="7f4c2-111">Recommendation</span></span> | <span data-ttu-id="7f4c2-112">Opis</span><span class="sxs-lookup"><span data-stu-id="7f4c2-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="7f4c2-113">Włączanie inspekcji i wykrywania zagrożeń na serwerach SQL</span><span class="sxs-lookup"><span data-stu-id="7f4c2-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="7f4c2-114">Zaleca się włączenie inspekcji i wykrywania zagrożeń dla serwerów SQL platformy Azure (usługą SQL platformy Azure; nie zawiera SQL uruchomionych na maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="7f4c2-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="7f4c2-115">Włączanie inspekcji i wykrywania zagrożeń w bazach danych SQL</span><span class="sxs-lookup"><span data-stu-id="7f4c2-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="7f4c2-116">Zaleca się włączenie inspekcji i wykrywania zagrożeń dla baz danych Azure SQL (usługą SQL platformy Azure; nie zawiera SQL uruchomionych na maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="7f4c2-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="7f4c2-117">Funkcja przezroczystego szyfrowania danych, Włącz bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="7f4c2-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="7f4c2-118">Zaleca się, aby włączyć szyfrowanie dla bazy danych SQL (tylko usługa Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="7f4c2-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="7f4c2-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7f4c2-119">See also</span></span>
<span data-ttu-id="7f4c2-120">toolearn więcej informacji na temat zaleceń, które są stosowane tooother typów zasobów platformy Azure, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7f4c2-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="7f4c2-121">Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="7f4c2-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="7f4c2-122">Ochrona aplikacji w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="7f4c2-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="7f4c2-123">Ochrona sieci w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="7f4c2-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="7f4c2-124">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7f4c2-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="7f4c2-125">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7f4c2-126">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7f4c2-127">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="7f4c2-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
