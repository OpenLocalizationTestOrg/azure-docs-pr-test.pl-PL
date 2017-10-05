---
title: "Inicjowanie obsługi aplikacji z filtrami zakresów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać filtrów zakresu, aby zapobiec obiektów w aplikacji, które obsługują Inicjowanie obsługi użytkowników automatycznych z faktycznie obsługiwana administracyjnie, jeśli obiekt nie spełniają wymagań biznesowych."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="29594-103">Udostępniania aplikacji na podstawie atrybutów z filtrami zakresów</span><span class="sxs-lookup"><span data-stu-id="29594-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="29594-104">Celem tej sekcji jest wyjaśnienie, jak używać filtrów zakresu do definiowania reguł na podstawie atrybutów, które określają, użytkowników, którzy są udostępnione do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29594-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="29594-105">Klauzule i zakres grupy</span><span class="sxs-lookup"><span data-stu-id="29594-105">Clauses and Scope Groups</span></span>
![Filtr zakresów][1] 

<span data-ttu-id="29594-107">Filtry zakresu są zdefiniowane przez jedną lub więcej **zakres grupy**, każdy z która zawiera jedną lub więcej **klauzule**.</span><span class="sxs-lookup"><span data-stu-id="29594-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="29594-108">Aby wyświetlić klauzule dla określonego zakresu grupy, rozwiń węzeł, klikając strzałkę w lewo nazwę grupy.</span><span class="sxs-lookup"><span data-stu-id="29594-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="29594-109">A **klauzuli** określa użytkowników, którzy mogą przekazywać zakresu filtru wyniku obliczenia atrybutów każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29594-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="29594-110">Na przykład może być jedną klauzulę, która wymaga atrybutu 'state' użytkownika równa Nowym Jorku, dzięki udostępnieniu tylko użytkownicy z nowego Jorku do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29594-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Nazwa grupy ustalania zakresu][2] 

<span data-ttu-id="29594-112">Każdy **grupy zakresu** rozpoczynają się od jednego obowiązkowe **klauzuli**, jak pokazano na zrzucie ekranu powyżej.</span><span class="sxs-lookup"><span data-stu-id="29594-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="29594-113">Po prostu klauzulę stwierdza, że użytkownik należy przypisać do aplikacji przed jej jest oceniana przez filtry zakresu.</span><span class="sxs-lookup"><span data-stu-id="29594-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="29594-114">Klauzulę nie można usunąć lub zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="29594-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="29594-115">Naciskając odpowiedni przycisk, można dodać nowe klauzule lub nowych grup zakresu.</span><span class="sxs-lookup"><span data-stu-id="29594-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="29594-116">Można nadać każdej grupy zakresu nazwę, edytując jej **Nazwa grupy zakresu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="29594-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="29594-117">Jak są analizowane filtry zakresu</span><span class="sxs-lookup"><span data-stu-id="29594-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="29594-118">Podczas inicjowania obsługi, firma Microsoft testuje co przypisany użytkownik względem filtry zakresu, aby ustalić, czy ten użytkownik wymaga dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29594-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="29594-119">Można potraktować każdej klauzuli jako testu, które muszą być przekazywane w kolejności dla użytkownika uniknąć pobierania odfiltrowane.</span><span class="sxs-lookup"><span data-stu-id="29594-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="29594-120">Jeśli masz wiele zdefiniowanych grup zakresu, każdy użytkownik musi przejść pomyślnie co najmniej jeden z nich, aby uzyskać dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29594-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="29594-121">Jednak w poszczególnych grupach zakresu, użytkownik musi mieć co klauzuli do przekazania tej grupy określonego zakresu.</span><span class="sxs-lookup"><span data-stu-id="29594-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="29594-122">Innymi słowy, można traktować zakres grupy jako połączone funkcją logiczną lub uważasz klauzul w nich jako i połączone funkcją logiczną.</span><span class="sxs-lookup"><span data-stu-id="29594-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="29594-123">Rozważmy na przykład Filtr zakresu poniżej:</span><span class="sxs-lookup"><span data-stu-id="29594-123">For example, consider the scoping filter below:</span></span>

![Nazwa grupy ustalania zakresu][3]  

<span data-ttu-id="29594-125">Zgodnie z tego zakresu filtru użytkownicy muszą spełniać następujące kryteria, można zainicjować obsługi administracyjnej:</span><span class="sxs-lookup"><span data-stu-id="29594-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="29594-126">Należy do nich przypisać do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29594-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="29594-127">Muszą one pracować z działu inżynierii</span><span class="sxs-lookup"><span data-stu-id="29594-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="29594-128">Muszą one być pracy w sieci San Francisco lub Kanady.</span><span class="sxs-lookup"><span data-stu-id="29594-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="29594-129">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="29594-129">Related Articles</span></span>
* [<span data-ttu-id="29594-130">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29594-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="29594-131">Automatyzowanie użytkownika alokowania i anulowania alokowania do aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="29594-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="29594-132">Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="29594-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="29594-133">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="29594-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="29594-134">Powiadomienia aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="29594-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="29594-135">Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM</span><span class="sxs-lookup"><span data-stu-id="29594-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="29594-136">Lista samouczków dotyczących sposobów integracji aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="29594-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
