---
title: "Ochrona usługi Azure SQL i danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="0c833-103">Ochrona usługi Azure SQL i danych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="0c833-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="0c833-104">Centrum zabezpieczeń Azure analizuje stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0c833-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="0c833-105">Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania wymaganych elementów sterujących.</span><span class="sxs-lookup"><span data-stu-id="0c833-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="0c833-106">Zalecenia dotyczą typów zasobów platformy Azure: maszynach wirtualnych (VM), sieci, SQL i danych i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c833-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="0c833-107">W tym artykule opisano zaleceń, które są stosowane do danych i usługą SQL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0c833-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="0c833-108">Zalecenia Centrum wokół Włączanie inspekcji baz danych, włączenie szyfrowania dla baz danych i włączenie szyfrowania konta magazynu Azure i serwerów SQL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0c833-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="0c833-109">Użyj poniższej tabeli jako odwołanie, aby lepiej zrozumieć dostępne zalecenia usługi i danych SQL i jak każdą z nich działa w przypadku zastosowania.</span><span class="sxs-lookup"><span data-stu-id="0c833-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="0c833-110">Dostępne zalecenia usługi i danych SQL</span><span class="sxs-lookup"><span data-stu-id="0c833-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="0c833-111">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="0c833-111">Recommendation</span></span> | <span data-ttu-id="0c833-112">Opis</span><span class="sxs-lookup"><span data-stu-id="0c833-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0c833-113">Włączanie inspekcji i wykrywania zagrożeń na serwerach SQL</span><span class="sxs-lookup"><span data-stu-id="0c833-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="0c833-114">Zaleca się włączenie inspekcji i wykrywania zagrożeń dla serwerów SQL platformy Azure (usługą SQL platformy Azure; nie zawiera SQL uruchomionych na maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="0c833-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="0c833-115">Włączanie inspekcji i wykrywania zagrożeń w bazach danych SQL</span><span class="sxs-lookup"><span data-stu-id="0c833-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="0c833-116">Zaleca się włączenie inspekcji i wykrywania zagrożeń dla baz danych Azure SQL (usługą SQL platformy Azure; nie zawiera SQL uruchomionych na maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="0c833-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="0c833-117">Funkcja przezroczystego szyfrowania danych, Włącz bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="0c833-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="0c833-118">Zaleca się, aby włączyć szyfrowanie dla bazy danych SQL (tylko usługa Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="0c833-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="0c833-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0c833-119">See also</span></span>
<span data-ttu-id="0c833-120">Aby dowiedzieć się więcej na temat zaleceń, które są stosowane do innych typów zasobów platformy Azure, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="0c833-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="0c833-121">Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="0c833-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="0c833-122">Ochrona aplikacji w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="0c833-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="0c833-123">Ochrona sieci w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="0c833-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="0c833-124">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="0c833-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="0c833-125">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0c833-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0c833-126">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="0c833-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="0c833-127">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="0c833-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
