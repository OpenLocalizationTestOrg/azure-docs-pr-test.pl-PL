---
title: "lokalizacje aaaNamed w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurując o nazwie lokalizacji, możesz uniknąć IP adresów, które są własnością organizacji wygenerować fałszywych alarmów dla lokalizacji tooatypical niemożliwa podróż hello ryzyka typ zdarzenia."
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
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="88106-103">Nazwane lokalizacje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88106-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="88106-104">Z hello o nazwie lokalizacji funkcji usługi Azure Active Directory można opisać zaufanych zakresów adresów IP w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="88106-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="88106-105">W danym środowisku, można użyć nazwane lokalizacje w kontekście hello wykrywanie hello [ryzyka zdarzenia](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="88106-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="88106-106">Witaj pomaga zmniejszyć hello liczbę fałszywych alarmów zgłoszone dla hello *lokalizacje tooatypical niemożliwa podróż* ryzyka typ zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="88106-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="88106-107">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="88106-107">Configuration</span></span>

<span data-ttu-id="88106-108">tooconfigure lokalizacji o nazwie:</span><span class="sxs-lookup"><span data-stu-id="88106-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="88106-109">Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="88106-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="88106-110">W okienku po lewej stronie powitania kliknij **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88106-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory łącze w okienku po lewej stronie powitania](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="88106-112">Na powitania **usługi Azure Active Directory** bloku w hello **zabezpieczeń** kliknij **dostępu warunkowego**.</span><span class="sxs-lookup"><span data-stu-id="88106-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Witaj polecenie dostępu warunkowego](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="88106-114">Na powitania **dostępu warunkowego** bloku w hello **Zarządzaj** kliknij **o nazwie lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="88106-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Witaj polecenia lokalizacji o nazwie](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="88106-116">Na powitania **o nazwie lokalizacje** bloku, kliknij przycisk **nową lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="88106-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Witaj nowe polecenie lokalizacji](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="88106-118">Na powitania **nowy** bloku hello następujące:</span><span class="sxs-lookup"><span data-stu-id="88106-118">On hello **New** blade, do hello following:</span></span>

    ![Nowy blok Hello](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="88106-120">a.</span><span class="sxs-lookup"><span data-stu-id="88106-120">a.</span></span> <span data-ttu-id="88106-121">W hello **nazwa** wpisz nazwę dla nazwanego lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="88106-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="88106-122">b.</span><span class="sxs-lookup"><span data-stu-id="88106-122">b.</span></span> <span data-ttu-id="88106-123">W hello **zakresów IP** wpisz zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="88106-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="88106-124">zakres adresów IP Hello musi toobe w hello *Bezklasowego routingu międzydomenowego* formacie (CIDR).</span><span class="sxs-lookup"><span data-stu-id="88106-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="88106-125">c.</span><span class="sxs-lookup"><span data-stu-id="88106-125">c.</span></span> <span data-ttu-id="88106-126">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="88106-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="88106-127">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="88106-127">What you should know</span></span>

<span data-ttu-id="88106-128">**Aktualizacje zbiorcze**: tworzenia lub aktualizowania nazwane lokalizacje aktualizacji zbiorczej można przekazać lub pobrania pliku CSV hello zakresów adresów IP.</span><span class="sxs-lookup"><span data-stu-id="88106-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="88106-129">Przekazanie dodaje zakresów IP hello hello pliku toohello listy zamiast zastępowanie hello listy.</span><span class="sxs-lookup"><span data-stu-id="88106-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Witaj, przekazywanie i pobieranie łącza](./media/active-directory-named-locations/09.png)


<span data-ttu-id="88106-131">**Ograniczenia**: można określić maksymalnie 60 nazwane lokalizacje, z jedną tooeach zakresu przypisanego adresu IP z nich.</span><span class="sxs-lookup"><span data-stu-id="88106-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="88106-132">Jeśli masz tylko jedną lokalizację o nazwie skonfigurowane dla niego można zdefiniować się too500 zakresów adresów IP.</span><span class="sxs-lookup"><span data-stu-id="88106-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="88106-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88106-133">Next steps</span></span>

<span data-ttu-id="88106-134">toolearn więcej informacji na temat zdarzeń o podwyższonym ryzyku, zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="88106-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

