---
title: "Przy użyciu usługi New Relic w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi New Relic do zarządzania i monitorowania aplikacji platformy Azure."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="dcbb2-103">Zarządzanie wydajnością aplikacji Relic nowego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="dcbb2-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="dcbb2-104">Możesz dodać światowej klasy wydajności usługi New Relic monitorowania do platformy Azure hostowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="dcbb2-105">Wraz z kompleksowe funkcje monitorowania i rozwiązywania problemów Dostrajanie aplikacji Azure przysługuje Ci również obniżonej cenie usługi New Relic produktów za pomocą usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="dcbb2-106">Co to jest usługi New Relic?</span><span class="sxs-lookup"><span data-stu-id="dcbb2-106">What is New Relic?</span></span>
<span data-ttu-id="dcbb2-107">Z [produktów usługi New Relic](https://newrelic.com/products), można naprawić błędy aplikacji, zapobiegać potencjalnych problemów i zrozumieć wydajność całego środowiska.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="dcbb2-108">Zostało zaprojektowane, aby oszczędzać czas potrzebny do rozpoznawania i diagnozowania problemów z wydajnością. Dzięki niemu informacje potrzebne do rozwiązania tych problemów znajdują się w zasięgu ręki.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="dcbb2-109">Usługi New Relic śledzi czas ładowania i Przepływność dla transakcji sieci web, zarówno z serwera i przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="dcbb2-110">Przedstawia on czas trwania w bazie danych, analizuje zapytania powolne i żądań sieci web, zawiera czas działania monitorowania i alertów, wyjątki aplikacji ścieżek i wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="dcbb2-111">Cennik specjalne</span><span class="sxs-lookup"><span data-stu-id="dcbb2-111">Special pricing</span></span>
<span data-ttu-id="dcbb2-112">Nowy Relic Standard jest bezpłatna dla użytkowników platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="dcbb2-113">Nowe Relic Pro jest oferowana w oparciu o rozmiar wystąpienia dla usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="dcbb2-114">Aby uzyskać informacje o cenach, zobacz [strony usługi New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) w portalu Azure Marketplace lub skontaktuj się z usługi New Relic (sales@newrelic.com) dla przedsiębiorstw cennik.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="dcbb2-115">Azure klientom Pro Relic nowej subskrypcji wersji próbnej dwóch tygodni po wdrożeniu przez nich agenta usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="dcbb2-116">Załóż konto usługi New Relic przy użyciu magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="dcbb2-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="dcbb2-117">Usługi New Relic bezproblemowo integruje się z rolami Azure ról sieć Web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="dcbb2-118">Można szybko i łatwo utworzyć konto usługi New Relic bezpośrednio w sklepie Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="dcbb2-119">Aby uzyskać instrukcje, zobacz [instrukcje tworzenia konta magazynu Azure](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) z usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="dcbb2-120">Wyświetlanie danych</span><span class="sxs-lookup"><span data-stu-id="dcbb2-120">View your data</span></span>
<span data-ttu-id="dcbb2-121">Po zarejestrowaniu się możesz korzystać z usługi New Relic niesamowite monitorowania aplikacji i analizy opartych na danych.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="dcbb2-122">Aby sprawdzić wydajność aplikacji w usługi New Relic:</span><span class="sxs-lookup"><span data-stu-id="dcbb2-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="dcbb2-123">Wybierz zarządzanie z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="dcbb2-124">Zaloguj się przy użyciu Twój adres e-mail konta usługi New Relic i hasło.</span><span class="sxs-lookup"><span data-stu-id="dcbb2-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="dcbb2-125">Wybierz aplikację z indeksu aplikacji, aby wyświetlić dane wszystkich aplikacji w [strony Przegląd APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="dcbb2-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="dcbb2-126">Przy użyciu usługi New Relic w usłudze Azure</span><span class="sxs-lookup"><span data-stu-id="dcbb2-126">Using New Relic with Azure</span></span>
<span data-ttu-id="dcbb2-127">Aby uzyskać więcej informacji na temat korzystania z usługi New Relic i Azure, zobacz [witryna dokumentacji usługi New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), takie jak:</span><span class="sxs-lookup"><span data-stu-id="dcbb2-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="dcbb2-128">Usługi New Relic dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="dcbb2-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="dcbb2-129">Instrumentacja roli procesu roboczego platformy .NET w usłudze w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="dcbb2-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="dcbb2-130">Usługi New Relic na platformie Microsoft Azure Cloud</span><span class="sxs-lookup"><span data-stu-id="dcbb2-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="dcbb2-131">Usługi New Relic dla aplikacji platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dcbb2-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="dcbb2-132">Rozwiązywanie problemów z nowego Relic/Azure</span><span class="sxs-lookup"><span data-stu-id="dcbb2-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

