---
title: "aaaData zasady dostępu w usłudze Azure czas serii Insights | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, zasady dostępu do danych toomanage w czasie serii Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="01e5e-103">Udziel dostępu danych tooa Insights serii czasu środowiska przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="01e5e-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="01e5e-104">Środowiska usługi Time Series Insights udostępniają dwa niezależne rodzaje zasad dostępu:</span><span class="sxs-lookup"><span data-stu-id="01e5e-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="01e5e-105">Zasady dostępu do zarządzania</span><span class="sxs-lookup"><span data-stu-id="01e5e-105">Management access policies</span></span>
* <span data-ttu-id="01e5e-106">Zasady dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="01e5e-106">Data access policies</span></span>

<span data-ttu-id="01e5e-107">Oba rodzaje zasad umożliwiają przyznawanie podmiotom usługi Azure Active Directory (użytkownikom i aplikacjom) różnych uprawnień w określonym środowisku.</span><span class="sxs-lookup"><span data-stu-id="01e5e-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="01e5e-108">Hello podmiotów zabezpieczeń (Użytkownicy i aplikacje) muszą należeć toohello active directory (lub "Dzierżawą platformy Azure") skojarzone z subskrypcją hello zawierający hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="01e5e-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="01e5e-109">Zasady dostępu administracyjnego przyznać uprawnienia powiązane toohello konfiguracji środowiska hello, takich jak</span><span class="sxs-lookup"><span data-stu-id="01e5e-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="01e5e-110">Tworzenie i usuwanie środowiska hello źródła zdarzeń odwołania zestawów danych i</span><span class="sxs-lookup"><span data-stu-id="01e5e-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="01e5e-111">Zarządzanie zasadami dostępu hello danych.</span><span class="sxs-lookup"><span data-stu-id="01e5e-111">Management of hello data access policies.</span></span>

<span data-ttu-id="01e5e-112">Zasady dostępu do danych uprawnienia tooissue kwerend danych, manipulować danymi odwołania w środowisku hello i udostępniaj zapisane kwerendy oraz skojarzone ze środowiskiem hello perspektywy.</span><span class="sxs-lookup"><span data-stu-id="01e5e-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="01e5e-113">Witaj dwa rodzaje zasady Zezwalaj wyraźnej separacji między zarządzania dostępem toohello hello środowiska i uzyskiwanie dostępu do danych toohello w środowisku hello.</span><span class="sxs-lookup"><span data-stu-id="01e5e-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="01e5e-114">Na przykład jest możliwe toosetup środowisko tak, aby hello właściciela/twórcy środowiska hello jest usuwany z hello dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="01e5e-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="01e5e-115">Oraz użytkowników i usług, które mogą tooread dane ze środowiska hello udziela się żadna konfiguracja toohello dostępu hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="01e5e-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="01e5e-116">Przyznawanie dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="01e5e-116">Grant data access</span></span>
<span data-ttu-id="01e5e-117">Witaj poniższej procedurze pokazano, jak toogrant dane — dostęp do głównej nazwy użytkownika:</span><span class="sxs-lookup"><span data-stu-id="01e5e-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="01e5e-118">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01e5e-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="01e5e-119">Kliknij przycisk "Wszystkie zasoby" hello menu po lewej stronie powitania hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="01e5e-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="01e5e-120">Wybierz środowisko usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="01e5e-120">Select your Time Series Insights environment.</span></span>

  ![Zarządzanie źródło czasu serii Insights hello - środowiska](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="01e5e-122">Wybierz pozycję „Dostęp do płaszczyzny danych” i kliknij przycisk „Dodaj”.</span><span class="sxs-lookup"><span data-stu-id="01e5e-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Zarządzanie źródła czasu serii Insights hello — Dodawanie](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="01e5e-124">Kliknij przycisk „Wybierz użytkownika”.</span><span class="sxs-lookup"><span data-stu-id="01e5e-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="01e5e-125">Wyszukiwanie i wybrać użytkownika, powitalne wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="01e5e-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="01e5e-126">Kliknij pozycję „Wybierz” w bloku „Wybierz użytkownika”.</span><span class="sxs-lookup"><span data-stu-id="01e5e-126">Click “Select” in “Select User” blade.</span></span>

  ![Zarządzanie źródła czasu serii Insights hello — wybierz użytkownika](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="01e5e-128">Kliknij pozycję „Wybierz rolę”.</span><span class="sxs-lookup"><span data-stu-id="01e5e-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="01e5e-129">Wybierz "Współautora", jeśli chcesz tooallow użytkownika toochange odwołanie do danych i udostępniać innym użytkownikom środowiska hello perspektyw i zapisane kwerendy.</span><span class="sxs-lookup"><span data-stu-id="01e5e-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="01e5e-130">W przeciwnym razie wybierz "Czytnika" tooallow użytkownika kwerend danych w środowisku hello i zapisać osobiste (nie udostępnione) zapytania w środowisku hello.</span><span class="sxs-lookup"><span data-stu-id="01e5e-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="01e5e-131">Kliknij przycisk Ok, w bloku "Wybierz rolę" hello.</span><span class="sxs-lookup"><span data-stu-id="01e5e-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Zarządzanie hello czasu serii Insights źródło - wybierz rolę](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="01e5e-133">Kliknij przycisk Ok, w bloku "Wybierz rolę użytkownika" hello.</span><span class="sxs-lookup"><span data-stu-id="01e5e-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="01e5e-134">Powinien zostać wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="01e5e-134">You should see:</span></span>

  ![Zarządzanie hello czasu serii Insights źródło - wyników](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="01e5e-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01e5e-136">Next steps</span></span>

* [<span data-ttu-id="01e5e-137">Tworzenie źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="01e5e-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="01e5e-138">[Wysyłanie zdarzeń](time-series-insights-send-events.md) toohello źródło zdarzenia</span><span class="sxs-lookup"><span data-stu-id="01e5e-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="01e5e-139">Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="01e5e-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
