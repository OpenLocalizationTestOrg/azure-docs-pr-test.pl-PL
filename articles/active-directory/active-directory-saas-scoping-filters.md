---
title: "aplikacje aaaProvisioning z filtrami zakresów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zakres toouse filtry tooprevent obiektów w aplikacji, które obsługują Inicjowanie obsługi użytkowników automatycznych z faktycznie obsługiwana administracyjnie, jeśli obiekt nie spełniają wymagań biznesowych."
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
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="8bcf2-103">Udostępniania aplikacji na podstawie atrybutów z filtrami zakresów</span><span class="sxs-lookup"><span data-stu-id="8bcf2-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="8bcf2-104">Celem Hello w tej sekcji jest tooexplain sposób określania zakresu toouse filtry toodefine atrybut reguły określające, którzy użytkownicy są udostępniane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="8bcf2-105">Klauzule i zakres grupy</span><span class="sxs-lookup"><span data-stu-id="8bcf2-105">Clauses and Scope Groups</span></span>
![Filtr zakresów][1] 

<span data-ttu-id="8bcf2-107">Filtry zakresu są zdefiniowane przez jedną lub więcej **zakres grupy**, każdy z która zawiera jedną lub więcej **klauzule**.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="8bcf2-108">klauzule hello toosee dla określonego zakresu grupy, rozwiń ją, klikając hello Strzałka toohello po lewej stronie powitania grupy nazwy.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="8bcf2-109">A **klauzuli** Określa, które użytkownicy mogą toopass za pośrednictwem hello zakresu filtru wyniku obliczenia atrybutów każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="8bcf2-110">Na przykład może zajść jedną klauzulę, który wymaga, aby użytkownika 'state' atrybutów równy Nowym Jorku, więc tylko użytkownicy z nowego Jorku są udostępnione do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Nazwa grupy ustalania zakresu][2] 

<span data-ttu-id="8bcf2-112">Każdy **grupy zakresu** rozpoczynają się od jednego obowiązkowe **klauzuli**, jak pokazano na powitania zrzucie ekranu pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="8bcf2-113">Klauzulę po prostu z informacją, że użytkownik hello należy przypisać toohello aplikacji przed jej jest oceniana przez filtry zakresu.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="8bcf2-114">Klauzulę nie można usunąć lub zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="8bcf2-115">Naciskając przycisk odpowiednie hello można dodać nowe klauzule lub nowych grup zakresu.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="8bcf2-116">Można nadać każdej grupy zakresu nazwę, edytując jej **Nazwa grupy zakresu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="8bcf2-117">Jak są analizowane filtry zakresu</span><span class="sxs-lookup"><span data-stu-id="8bcf2-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="8bcf2-118">Podczas inicjowania obsługi, firma Microsoft testuje co przypisany użytkownik względem z zakresu toodetermine filtrów, jeśli użytkownik wymaga dostępu toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="8bcf2-119">Można potraktować każdej klauzuli jako test, który musi zostać przekazane, tooavoid użytkownika hello pobierania odfiltrowane.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="8bcf2-120">Jeśli masz wiele zdefiniowanych grup zakresu, każdy użytkownik musi przejść pomyślnie co najmniej jeden z nich tooaccess aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="8bcf2-121">W każdej grupie zakresu jednak hello użytkownik musi mieć co toopass klauzuli tej grupy określonego zakresu.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="8bcf2-122">Innymi słowy, można traktować zakres grupy jako połączone funkcją logiczną lub można traktować klauzule hello w nich jako i połączone funkcją logiczną.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="8bcf2-123">Rozważmy na przykład hello zakresu filtru poniżej:</span><span class="sxs-lookup"><span data-stu-id="8bcf2-123">For example, consider hello scoping filter below:</span></span>

![Nazwa grupy ustalania zakresu][3]  

<span data-ttu-id="8bcf2-125">Zgodnie z toothis zakresu filtru, użytkownicy muszą spełniać następujące hello kryteria, toobe obsługi administracyjnej:</span><span class="sxs-lookup"><span data-stu-id="8bcf2-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="8bcf2-126">Musi mieć przypisaną toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="8bcf2-127">Muszą one działać działu inżynierii hello</span><span class="sxs-lookup"><span data-stu-id="8bcf2-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="8bcf2-128">Muszą one być pracy w sieci San Francisco lub Kanady.</span><span class="sxs-lookup"><span data-stu-id="8bcf2-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="8bcf2-129">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="8bcf2-129">Related Articles</span></span>
* [<span data-ttu-id="8bcf2-130">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bcf2-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="8bcf2-131">Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji</span><span class="sxs-lookup"><span data-stu-id="8bcf2-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="8bcf2-132">Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="8bcf2-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="8bcf2-133">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="8bcf2-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="8bcf2-134">Powiadomienia aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="8bcf2-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="8bcf2-135">Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="8bcf2-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="8bcf2-136">Lista samouczków dotyczących tooIntegrate aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="8bcf2-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
