---
title: "Utwórz partnerów wiadomości między firmami (B2B) - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać partnerów do swojego konta integracji z pakiet integracyjny dla przedsiębiorstw i Logic Apps"
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
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="cc161-103">Dodaj lub zaktualizuj partnerów w umowach business-to-business w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="cc161-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="cc161-104">Partnerzy to podmiotom uczestniczenie w transakcjach (B2B) business-to-business i wymiany wiadomości między sobą.</span><span class="sxs-lookup"><span data-stu-id="cc161-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="cc161-105">Przed utworzeniem partnerów, które reprezentują i innej organizacji w tych transakcji, należy najpierw zarówno udostępnianie informacji, która identyfikuje i weryfikuje komunikatów wysłanych przez siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="cc161-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="cc161-106">Po omówiono te szczegóły i zacząć z firmą, można utworzyć partnerów na koncie integracji do reprezentowania obie.</span><span class="sxs-lookup"><span data-stu-id="cc161-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="cc161-107">Jakie role partnerów masz na koncie integracji?</span><span class="sxs-lookup"><span data-stu-id="cc161-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="cc161-108">Zdefiniuj szczegóły wiadomości wymieniane między partnerami, utworzysz umów tych partnerów.</span><span class="sxs-lookup"><span data-stu-id="cc161-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="cc161-109">Jednakże przed utworzeniem umowę, należy dodać co najmniej dwie firmy partnerskie do swojego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="cc161-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="cc161-110">Twoja organizacja musi być częścią umowy jako **partnera hosta**.</span><span class="sxs-lookup"><span data-stu-id="cc161-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="cc161-111">Drugiego partnera, lub **partnera gościa** to organizacja, który wymienia wiadomości w swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="cc161-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="cc161-112">Partner gościa może być innej firmy lub nawet działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="cc161-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="cc161-113">Po dodaniu tych partnerów, można utworzyć umowy.</span><span class="sxs-lookup"><span data-stu-id="cc161-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="cc161-114">Odbierania i wysyłania, ustawienia są obiektowe z punktu widzenia hostowanej partnera.</span><span class="sxs-lookup"><span data-stu-id="cc161-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="cc161-115">Na przykład odbierania ustawienia w umowie określają sposób hostowanej partnera odbiera wiadomości wysyłane z partnerem gościa.</span><span class="sxs-lookup"><span data-stu-id="cc161-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="cc161-116">Podobnie, Wyślij ustawienia na umowie wskazują, jak hostowanej partner wysyła komunikaty do partnera gościa.</span><span class="sxs-lookup"><span data-stu-id="cc161-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="cc161-117">Jak utworzyć partnera?</span><span class="sxs-lookup"><span data-stu-id="cc161-117">How to create a partner?</span></span>

1. <span data-ttu-id="cc161-118">W portalu Azure wybierz **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="cc161-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="cc161-119">W polu filtru wyszukiwania wprowadź **integracji**, a następnie wybierz pozycję **konta integracji** na liście wyników.</span><span class="sxs-lookup"><span data-stu-id="cc161-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="cc161-120">Wybierz konto integracji, w której chcesz dodać partnerów.</span><span class="sxs-lookup"><span data-stu-id="cc161-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="cc161-121">Wybierz **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="cc161-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="cc161-122">W bloku partnerów, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cc161-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="cc161-123">Wprowadź nazwę dla partnera, a następnie wybierz **kwalifikator**.</span><span class="sxs-lookup"><span data-stu-id="cc161-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="cc161-124">Na koniec, wprowadź **wartość** ułatwia zidentyfikowanie dokumentów, które pochodzą ze swoimi aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="cc161-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="cc161-125">Aby wyświetlić postęp procesu tworzenia partnera, wybierz *dzwonka* ikonę powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="cc161-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="cc161-126">Aby potwierdzić pomyślnie dodano nowe partnerów, wybierz **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="cc161-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="cc161-127">Po wybraniu kafelka partnerów, widoczny będzie również nowo dodanego partnerów w bloku partnerów.</span><span class="sxs-lookup"><span data-stu-id="cc161-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="cc161-128">Jak edytować istniejących partnerów w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="cc161-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="cc161-129">Wybierz **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="cc161-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="cc161-130">Po otwarciu bloku partnerów, wybierz partnera, który chcesz edytować.</span><span class="sxs-lookup"><span data-stu-id="cc161-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="cc161-131">Na **partnera aktualizacji** kafelka, wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="cc161-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="cc161-132">Po zakończeniu wybierz **zapisać**, lub Anuluj zmiany, wybierz **odrzucić**.</span><span class="sxs-lookup"><span data-stu-id="cc161-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="cc161-133">Jak usunąć partnera</span><span class="sxs-lookup"><span data-stu-id="cc161-133">How to delete a partner</span></span>

1. <span data-ttu-id="cc161-134">Wybierz **partnerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="cc161-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="cc161-135">Po otwarciu bloku partnera, wybierz partnera, którego chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="cc161-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="cc161-136">Wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="cc161-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="cc161-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc161-137">Next steps</span></span>
* [<span data-ttu-id="cc161-138">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="cc161-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  

