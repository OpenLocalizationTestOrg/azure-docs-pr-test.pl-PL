---
title: "partnerzy aaaCreate wiadomości między firmami (B2B) - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konto tooadd partnerów tooyour integracji z hello pakiet integracyjny dla przedsiębiorstw i Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="b1235-103">Dodaj lub zaktualizuj partnerów w umowach business-to-business w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="b1235-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="b1235-104">Partnerzy to podmiotom uczestniczenie w transakcjach (B2B) business-to-business i wymiany wiadomości między sobą.</span><span class="sxs-lookup"><span data-stu-id="b1235-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="b1235-105">Przed utworzeniem partnerów, które reprezentują i innej organizacji w tych transakcji, należy najpierw zarówno udostępnianie informacji, która identyfikuje i weryfikuje komunikatów wysłanych przez siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="b1235-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="b1235-106">Po omówiono te informacje i są gotowe toostart Twojego relacji biznesowej, można utworzyć partnerów w Twojej toorepresent konta integracji obie.</span><span class="sxs-lookup"><span data-stu-id="b1235-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="b1235-107">Jakie role partnerów masz na koncie integracji?</span><span class="sxs-lookup"><span data-stu-id="b1235-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="b1235-108">Szczegóły toodefine wiadomości powitania wymieniane między partnerami, Utwórz umów tych partnerów.</span><span class="sxs-lookup"><span data-stu-id="b1235-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="b1235-109">Jednak przed utworzeniem umowę, należy dodać co najmniej dwie firmy partnerskie tooyour integracji konta.</span><span class="sxs-lookup"><span data-stu-id="b1235-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="b1235-110">Twoja organizacja musi być częścią umowy hello jako hello **partnera hosta**.</span><span class="sxs-lookup"><span data-stu-id="b1235-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="b1235-111">Witaj drugiego partnera lub **partnera gościa** reprezentuje hello organizacji, który wymienia wiadomości w swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="b1235-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="b1235-112">Hello partnera gościa może być innej firmy lub nawet działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="b1235-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="b1235-113">Po dodaniu tych partnerów, można utworzyć umowy.</span><span class="sxs-lookup"><span data-stu-id="b1235-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="b1235-114">Odbierania i wysyłania, ustawienia są obiektowe z hello punktu widzenia hello hostowana partnera.</span><span class="sxs-lookup"><span data-stu-id="b1235-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="b1235-115">Na przykład hello odbierają ustawienia w umowie określić sposób partnera hello hostowanej odbiera wiadomości wysyłane z partnerem gościa.</span><span class="sxs-lookup"><span data-stu-id="b1235-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="b1235-116">Podobnie, hello wysyłania ustawienia na umowie hello wskazują, jak hello hostowanej partner wysyła wiadomości toohello gościa partnera.</span><span class="sxs-lookup"><span data-stu-id="b1235-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="b1235-117">Jak toocreate partnera?</span><span class="sxs-lookup"><span data-stu-id="b1235-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="b1235-118">Hello portalu Azure, wybierz **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="b1235-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="b1235-119">W polu wyszukiwania filtr hello, wprowadź **integracji**, a następnie wybierz pozycję **konta integracji** hello listy wyników.</span><span class="sxs-lookup"><span data-stu-id="b1235-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="b1235-120">Wybierz konto integracji hello miejscu tooadd partnerów.</span><span class="sxs-lookup"><span data-stu-id="b1235-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="b1235-121">Wybierz hello **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b1235-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="b1235-122">W bloku partnerów hello, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b1235-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="b1235-123">Wprowadź nazwę dla partnera, a następnie wybierz **kwalifikator**.</span><span class="sxs-lookup"><span data-stu-id="b1235-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="b1235-124">Na koniec, wprowadź **wartość** toohelp określenie dokumentów, które pochodzą ze swoimi aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="b1235-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="b1235-125">postęp hello toosee partnera proces tworzenia, wybierz hello *dzwonka* ikonę powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="b1235-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="b1235-126">tooconfirm, który partnerów nowe pomyślnie zostały dodane, wybierz hello **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b1235-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="b1235-127">Po wybraniu kafelka partnerów hello sekcji omówiono również, nowo dodanego partnerów w bloku partnerów hello.</span><span class="sxs-lookup"><span data-stu-id="b1235-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="b1235-128">Jak istniejące tooedit partnerzy na koncie integracji</span><span class="sxs-lookup"><span data-stu-id="b1235-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="b1235-129">Wybierz hello **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b1235-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="b1235-130">Po otwarciu bloku partnerów hello wybierz partnera hello ma tooedit.</span><span class="sxs-lookup"><span data-stu-id="b1235-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="b1235-131">Na powitania **partnera aktualizacji** kafelka, wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="b1235-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="b1235-132">Po zakończeniu wybierz **zapisać**, lub wybierz zmiany, toocancel **odrzucić**.</span><span class="sxs-lookup"><span data-stu-id="b1235-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="b1235-133">Jak toodelete partnera</span><span class="sxs-lookup"><span data-stu-id="b1235-133">How toodelete a partner</span></span>

1. <span data-ttu-id="b1235-134">Wybierz hello **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b1235-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="b1235-135">Po otwarciu bloku partnera hello wybierz hello partnera, które mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="b1235-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="b1235-136">Wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b1235-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="b1235-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1235-137">Next steps</span></span>
* [<span data-ttu-id="b1235-138">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="b1235-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  

