---
title: "Umowy dotyczące komunikacji B2B - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie umów, partnerzy mogą komunikować się w scenariusze B2B usługi Azure Logic Apps i pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="30b63-103">Umowy z partnerami komunikacji B2B usługi Azure Logic Apps i pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="30b63-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="30b63-104">Umowy pozwalają jednostki biznesowe, które komunikują się bezproblemowo przy użyciu standardowych protokołach branżowych i to podstawy komunikacji biznesowych między firmami (B2B).</span><span class="sxs-lookup"><span data-stu-id="30b63-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="30b63-105">Podczas włączania scenariusze B2B dla aplikacji logiki z pakiet integracyjny dla przedsiębiorstw, Umowa jest w układzie komunikacji między partnerami handlowymi B2B.</span><span class="sxs-lookup"><span data-stu-id="30b63-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="30b63-106">Niniejsza Umowa jest oparte na komunikacji, że partnerów chcesz ustanowić i protokół lub specyficznych dla transportu.</span><span class="sxs-lookup"><span data-stu-id="30b63-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="30b63-107">Integracja Enterprise obsługuje te standardy protokołu lub transportu:</span><span class="sxs-lookup"><span data-stu-id="30b63-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="30b63-108">AS2</span><span class="sxs-lookup"><span data-stu-id="30b63-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="30b63-109">X12</span><span class="sxs-lookup"><span data-stu-id="30b63-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="30b63-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="30b63-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="30b63-111">Dlaczego warto używać umów</span><span class="sxs-lookup"><span data-stu-id="30b63-111">Why use agreements</span></span>

<span data-ttu-id="30b63-112">Oto niektóre typowe korzyści, korzystając z umowy:</span><span class="sxs-lookup"><span data-stu-id="30b63-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="30b63-113">Umożliwia różnych organizacji i firm do wymiany informacji w formacie dobrze znany.</span><span class="sxs-lookup"><span data-stu-id="30b63-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="30b63-114">Zwiększa wydajność podczas przeprowadzania transakcji B2B</span><span class="sxs-lookup"><span data-stu-id="30b63-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="30b63-115">Łatwe do tworzenia, zarządzania i używać przy tworzeniu aplikacji integracji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="30b63-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="30b63-116">Tworzenie umów</span><span class="sxs-lookup"><span data-stu-id="30b63-116">How to create agreements</span></span>

* [<span data-ttu-id="30b63-117">Tworzenie umów AS2</span><span class="sxs-lookup"><span data-stu-id="30b63-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="30b63-118">Utwórz X12 umowy</span><span class="sxs-lookup"><span data-stu-id="30b63-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="30b63-119">Tworzenie umów EDIFACT</span><span class="sxs-lookup"><span data-stu-id="30b63-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="30b63-120">Jak używać umowy</span><span class="sxs-lookup"><span data-stu-id="30b63-120">How to use an agreement</span></span>

<span data-ttu-id="30b63-121">Można utworzyć [aplikacje logiki](logic-apps-what-are-logic-apps.md "Dowiedz się więcej o aplikacjach logiki") z możliwościami B2B za pomocą utworzonego umowy.</span><span class="sxs-lookup"><span data-stu-id="30b63-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="30b63-122">Jak edytować umowy</span><span class="sxs-lookup"><span data-stu-id="30b63-122">How to edit an agreement</span></span>

<span data-ttu-id="30b63-123">Wszystkie umowy można edytować, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="30b63-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="30b63-124">Wybierz konto integracji, które ma umowę, którą chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="30b63-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="30b63-125">Wybierz **umowy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="30b63-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="30b63-126">Na **umowy** bloku, wybierz umowy.</span><span class="sxs-lookup"><span data-stu-id="30b63-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="30b63-127">Wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="30b63-127">Choose **Edit**.</span></span> <span data-ttu-id="30b63-128">Wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="30b63-128">Make your changes.</span></span>

5. <span data-ttu-id="30b63-129">Aby zapisać zmiany, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="30b63-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="30b63-130">Jak usunąć umowy</span><span class="sxs-lookup"><span data-stu-id="30b63-130">How to delete an agreement</span></span>

<span data-ttu-id="30b63-131">Aby usunąć wszystkie umowy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="30b63-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="30b63-132">Wybierz konto integracji, które ma umowę, którą chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="30b63-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="30b63-133">Wybierz **umowy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="30b63-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="30b63-134">Na **umowy** bloku, wybierz umowy.</span><span class="sxs-lookup"><span data-stu-id="30b63-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="30b63-135">Wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="30b63-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="30b63-136">Upewnij się, że chcesz usunąć wybraną umowę.</span><span class="sxs-lookup"><span data-stu-id="30b63-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="30b63-137">Blok umów nie jest już wyświetlana usunięto umowy.</span><span class="sxs-lookup"><span data-stu-id="30b63-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30b63-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30b63-138">Next steps</span></span>
* [<span data-ttu-id="30b63-139">Tworzenie umów AS2</span><span class="sxs-lookup"><span data-stu-id="30b63-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
