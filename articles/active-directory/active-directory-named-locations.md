---
title: "O nazwie lokalizacjach w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurując o nazwie lokalizacji, możesz uniknąć generowanie adresów IP, które są własnością organizacji fałszywych alarmów dla Impossible podróż do nietypowych lokalizacji ryzyka zdarzeń typu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="69361-103">Nazwane lokalizacje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69361-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="69361-104">Dzięki funkcji o nazwie lokalizacji usługi Azure Active Directory można opisać zaufanych zakresów adresów IP w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="69361-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="69361-105">W danym środowisku, można użyć nazwane lokalizacje w kontekście wykrywania [ryzyka zdarzenia](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="69361-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="69361-106">Pomaga zmniejszyć liczbę fałszywych alarmów zgłoszone dla *Impossible podróż do nietypowych lokalizacji* ryzyka typ zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="69361-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="69361-107">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="69361-107">Configuration</span></span>

<span data-ttu-id="69361-108">Aby skonfigurować lokalizację o nazwie:</span><span class="sxs-lookup"><span data-stu-id="69361-108">To configure a named location:</span></span>

1. <span data-ttu-id="69361-109">Zaloguj się do [portalu Azure](https://portal.azure.com) jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="69361-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="69361-110">W okienku po lewej stronie kliknij **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="69361-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![Łącze usługi Azure Active Directory w okienku po lewej stronie](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="69361-112">Na **usługi Azure Active Directory** bloku, w **zabezpieczeń** kliknij **dostępu warunkowego**.</span><span class="sxs-lookup"><span data-stu-id="69361-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![Polecenie dostępu warunkowego](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="69361-114">Na **dostępu warunkowego** bloku, w **Zarządzaj** kliknij **o nazwie lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="69361-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![Polecenie lokalizacji o nazwie](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="69361-116">Na **o nazwie lokalizacje** bloku, kliknij przycisk **nową lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="69361-116">On the **Named locations** blade, click **New location**.</span></span>

    ![Nowe polecenie lokalizacji](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="69361-118">Na **nowy** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="69361-118">On the **New** blade, do the following:</span></span>

    ![Nowy blok](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="69361-120">a.</span><span class="sxs-lookup"><span data-stu-id="69361-120">a.</span></span> <span data-ttu-id="69361-121">W **nazwa** wpisz nazwę dla nazwanego lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="69361-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="69361-122">b.</span><span class="sxs-lookup"><span data-stu-id="69361-122">b.</span></span> <span data-ttu-id="69361-123">W **zakresów IP** wpisz zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="69361-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="69361-124">Zakres adresów IP musi być w *Bezklasowego routingu międzydomenowego* formacie (CIDR).</span><span class="sxs-lookup"><span data-stu-id="69361-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="69361-125">c.</span><span class="sxs-lookup"><span data-stu-id="69361-125">c.</span></span> <span data-ttu-id="69361-126">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="69361-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="69361-127">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="69361-127">What you should know</span></span>

<span data-ttu-id="69361-128">**Aktualizacje zbiorcze**: tworzenia lub aktualizowania nazwane lokalizacje aktualizacje zbiorcze, możesz przekazać lub pobrać plik CSV z zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="69361-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="69361-129">Przekazanie dodaje zakresu adresów IP w pliku do listy zamiast zastępowanie na liście.</span><span class="sxs-lookup"><span data-stu-id="69361-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Przekazywanie i pobieranie łącza](./media/active-directory-named-locations/09.png)


<span data-ttu-id="69361-131">**Ograniczenia**: można określić maksymalnie 60 nazwane lokalizacje, z jeden zakres adresów IP przypisanych do każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="69361-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="69361-132">Jeśli masz tylko jedną lokalizację o nazwie skonfigurowane do 500 zakresów adresów IP można zdefiniować dla niego.</span><span class="sxs-lookup"><span data-stu-id="69361-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="69361-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="69361-133">Next steps</span></span>

<span data-ttu-id="69361-134">Aby dowiedzieć się więcej na temat zdarzeń o podwyższonym ryzyku, zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="69361-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

