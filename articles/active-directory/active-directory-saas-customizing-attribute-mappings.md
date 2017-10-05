---
title: "Dostosowywanie mapowań atrybutów usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory są, jak można dostosować je do adresów potrzeb biznesowych."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="a4e32-103">Dostosowywanie użytkownika udostępniania mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4e32-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="a4e32-104">Inicjowanie obsługi użytkowników do aplikacji SaaS innych firm, takie jak Salesforce, Google Apps i innych użytkowników usługi Microsoft Azure AD zapewnia obsługę.</span><span class="sxs-lookup"><span data-stu-id="a4e32-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="a4e32-105">Jeśli masz użytkownika Inicjowanie obsługi administracyjnej dla aplikacji SaaS innych firm włączone portalu zarządzania Azure określa jego wartości atrybutów w postaci konfiguracji o nazwie "mapowanie atrybutu".</span><span class="sxs-lookup"><span data-stu-id="a4e32-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="a4e32-106">Brak zestawu wstępnie skonfigurowanych atrybutu mapowania między obiektami użytkownika usługi Azure AD i każda aplikacja SaaS użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4e32-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="a4e32-107">Niektóre aplikacje zarządzania innych typów obiektów, takich jak grup ani kontaktów.</span><span class="sxs-lookup"><span data-stu-id="a4e32-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="a4e32-108">Mapowanie atrybutów domyślne można dostosować zgodnie z potrzebami firmy.</span><span class="sxs-lookup"><span data-stu-id="a4e32-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="a4e32-109">Oznacza to, że możesz zmienić lub usunąć istniejące mapowania atrybutu lub utworzyć nowe mapowanie atrybutów.</span><span class="sxs-lookup"><span data-stu-id="a4e32-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="a4e32-110">W portalu usługi Azure AD, możesz korzystać z tej funkcji, klikając **mapowania** Konfiguracja **inicjowania obsługi administracyjnej** w **Zarządzaj** części  **Aplikacja całościowa**.</span><span class="sxs-lookup"><span data-stu-id="a4e32-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![SalesForce][5] 

<span data-ttu-id="a4e32-112">Kliknięcie przycisku **mapowania** konfiguracji, otwiera pokrewny **mapowanie atrybutu** bloku.</span><span class="sxs-lookup"><span data-stu-id="a4e32-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="a4e32-113">Brak mapowań atrybutów, które są wymagane przez aplikacji SaaS, aby mógł działać poprawnie.</span><span class="sxs-lookup"><span data-stu-id="a4e32-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="a4e32-114">Dla wymaganych atrybutów **usunąć** funkcja jest niedostępna.</span><span class="sxs-lookup"><span data-stu-id="a4e32-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![SalesForce][6]  

<span data-ttu-id="a4e32-116">W powyższym przykładzie można stwierdzić, że **Username** atrybutu zarządzanego obiektu w usłudze Salesforce jest wypełniana **userPrincipalName** wartość połączonego Azure obiektu usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4e32-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="a4e32-117">Można dostosować istniejący **mapowań atrybutów** klikając mapowania.</span><span class="sxs-lookup"><span data-stu-id="a4e32-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="a4e32-118">Spowoduje to otwarcie **atrybutu Edytuj** bloku.</span><span class="sxs-lookup"><span data-stu-id="a4e32-118">This opens the **Edit Attribute** blade.</span></span>

![SalesForce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="a4e32-120">Opis atrybutu mapowania typów</span><span class="sxs-lookup"><span data-stu-id="a4e32-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="a4e32-121">Z mapowań atrybutów możesz kontrolować sposób atrybuty są wypełnione w aplikacji SaaS innych firm.</span><span class="sxs-lookup"><span data-stu-id="a4e32-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="a4e32-122">Istnieją cztery typy innego mapowania obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="a4e32-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="a4e32-123">**Bezpośrednie** — atrybut docelowy jest wypełniane przy użyciu wartości atrybutu połączonego obiektu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4e32-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="a4e32-124">**Stała** — atrybut docelowy jest wypełniana określony ciąg został określony.</span><span class="sxs-lookup"><span data-stu-id="a4e32-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="a4e32-125">**Wyrażenie** — atrybut docelowy jest wypełniana na podstawie wyniku wyrażenia przypominającej skryptu.</span><span class="sxs-lookup"><span data-stu-id="a4e32-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="a4e32-126">Aby uzyskać więcej informacji, zobacz [pisać wyrażenia potrzeby mapowań atrybutów w usłudze Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="a4e32-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="a4e32-127">**Brak** — atrybut docelowy zostanie pozostawiony bez modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="a4e32-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="a4e32-128">Jednak jeśli atrybut docelowy jest kiedykolwiek pusta, jest wypełnione wartością domyślną, który określisz.</span><span class="sxs-lookup"><span data-stu-id="a4e32-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="a4e32-129">Oprócz tych cztery typy mapowanie atrybutu podstawowego mapowań atrybutów niestandardowych obsługuje pojęcie opcjonalny **domyślne** przypisanie wartości.</span><span class="sxs-lookup"><span data-stu-id="a4e32-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="a4e32-130">Przypisanie wartości domyślne gwarantuje, że atrybut docelowy jest wypełniana wartości, które nie istnieje żadna wartość w usłudze Azure AD, ani na obiekcie docelowym.</span><span class="sxs-lookup"><span data-stu-id="a4e32-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="a4e32-131">Najbardziej typowych konfiguracji jest to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="a4e32-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="a4e32-132">Opis właściwości Mapowanie atrybutów</span><span class="sxs-lookup"><span data-stu-id="a4e32-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="a4e32-133">W poprzedniej sekcji możesz już zostały wprowadzone do właściwości typu atrybutu mapowania.</span><span class="sxs-lookup"><span data-stu-id="a4e32-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="a4e32-134">Oprócz tej właściwości mapowań atrybutów obsługują następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="a4e32-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="a4e32-135">**Atrybut źródłowy** — atrybut użytkownika z systemu źródłowego (np.: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a4e32-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="a4e32-136">**Atrybut TARGET** — atrybut użytkownika w systemie docelowym (np.: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="a4e32-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="a4e32-137">**Zgodne obiektów przy użyciu tego atrybutu** — czy to mapowanie powinien być używany do jednoznacznego identyfikowania użytkowników między systemami źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="a4e32-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="a4e32-138">Jest to zazwyczaj ustawiana na atrybut userPrincipalName lub poczty w usłudze Azure AD, która zwykle jest mapowana na pole nazwy użytkownika w aplikacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="a4e32-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="a4e32-139">**Dopasowywanie pierwszeństwo** — wiele pasujących atrybuty można ustawić.</span><span class="sxs-lookup"><span data-stu-id="a4e32-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="a4e32-140">Jeśli dostępnych jest wiele, są oceniane pod w kolejności wynika z tego pola.</span><span class="sxs-lookup"><span data-stu-id="a4e32-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="a4e32-141">Jak dopasowania zostanie znaleziony, żadne dodatkowe dopasowania atrybuty są oceniane.</span><span class="sxs-lookup"><span data-stu-id="a4e32-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="a4e32-142">**Zastosuj to mapowanie**</span><span class="sxs-lookup"><span data-stu-id="a4e32-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="a4e32-143">**Zawsze** — Zastosuj to mapowanie na obu Tworzenie użytkownika i aktualizowanie akcji</span><span class="sxs-lookup"><span data-stu-id="a4e32-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="a4e32-144">**Tylko podczas tworzenia** -Zastosuj to mapowanie tylko akcje creation użytkownika</span><span class="sxs-lookup"><span data-stu-id="a4e32-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="a4e32-145">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="a4e32-145">What you should know</span></span>

<span data-ttu-id="a4e32-146">Microsoft Azure AD zapewnia wydajne wykonania procesu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="a4e32-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="a4e32-147">W środowisku zainicjowana tylko obiekty wymagające aktualizacji są przetwarzane podczas cyklu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="a4e32-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="a4e32-148">Aktualizowanie mapowań atrybutów ma wpływ na wydajność cyklu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="a4e32-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="a4e32-149">Aktualizacja konfiguracji mapowania atrybut wymaga wszystkich obiektów zarządzanych go obliczyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="a4e32-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="a4e32-150">Jest zalecanym najlepszym rozwiązaniem aby utrzymać liczbę kolejnych zmian do mapowania atrybutu co najmniej.</span><span class="sxs-lookup"><span data-stu-id="a4e32-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4e32-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4e32-151">Next steps</span></span>

* [<span data-ttu-id="a4e32-152">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4e32-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a4e32-153">Automatyzowanie użytkownika udostępniania/anulowania obsługi do aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="a4e32-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="a4e32-154">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="a4e32-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="a4e32-155">Filtry zakresu dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="a4e32-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="a4e32-156">Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM</span><span class="sxs-lookup"><span data-stu-id="a4e32-156">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="a4e32-157">Powiadomienia aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="a4e32-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="a4e32-158">Lista samouczków dotyczących sposobów integracji aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="a4e32-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

