---
title: "aaaCustomizing mapowań atrybutów AD Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory są, jak można je zmodyfikować tooaddress firmy wymaga."
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
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="ef0cc-103">Dostosowywanie użytkownika udostępniania mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef0cc-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="ef0cc-104">Microsoft Azure AD zapewnia obsługę aprowizacji aplikacji SaaS toothird firm, takie jak Salesforce, Google Apps i innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="ef0cc-105">Jeśli masz użytkownika Inicjowanie obsługi administracyjnej dla aplikacji SaaS innych firm włączone hello portalu zarządzania Azure określa jego wartości atrybutów w postaci konfiguracji o nazwie "mapowanie atrybutu".</span><span class="sxs-lookup"><span data-stu-id="ef0cc-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="ef0cc-106">Brak zestawu wstępnie skonfigurowanych atrybutu mapowania między obiektami użytkownika usługi Azure AD i każda aplikacja SaaS użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="ef0cc-107">Niektóre aplikacje zarządzania innych typów obiektów, takich jak grup ani kontaktów.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="ef0cc-108">Mapowanie atrybutów domyślne hello zgodnie z potrzebami biznesowymi tooyour można dostosować.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="ef0cc-109">Oznacza to, że możesz zmienić lub usunąć istniejące mapowania atrybutu lub utworzyć nowe mapowanie atrybutów.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="ef0cc-110">W portalu hello Azure AD, możesz korzystać z tej funkcji, klikając **mapowania** Konfiguracja **inicjowania obsługi administracyjnej** w hello **Zarządzaj** części  **Aplikacja całościowa**.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![SalesForce][5] 

<span data-ttu-id="ef0cc-112">Kliknięcie przycisku **mapowania** konfiguracji, otwiera hello powiązane **mapowanie atrybutu** bloku.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="ef0cc-113">Brak mapowań atrybutów, które są wymagane przez toofunction aplikacji SaaS poprawnie.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="ef0cc-114">Dla wymaganych atrybutów hello **usunąć** funkcja jest niedostępna.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![SalesForce][6]  

<span data-ttu-id="ef0cc-116">W powyższym przykładzie hello, widać, że hello **Username** atrybutu zarządzanego obiektu w usłudze Salesforce jest wypełniana hello **userPrincipalName** wartość hello połączonego obiektu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="ef0cc-117">Można dostosować istniejący **mapowań atrybutów** klikając mapowania.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="ef0cc-118">Spowoduje to otwarcie hello **atrybutu Edytuj** bloku.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-118">This opens hello **Edit Attribute** blade.</span></span>

![SalesForce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="ef0cc-120">Opis atrybutu mapowania typów</span><span class="sxs-lookup"><span data-stu-id="ef0cc-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="ef0cc-121">Z mapowań atrybutów możesz kontrolować sposób atrybuty są wypełnione w aplikacji SaaS innych firm.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="ef0cc-122">Istnieją cztery typy innego mapowania obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="ef0cc-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="ef0cc-123">**Bezpośrednie** — atrybut target hello jest wypełniana hello wartości atrybutu hello połączonego obiektu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="ef0cc-124">**Stała** — atrybut target hello jest wypełniana określony ciąg został określony.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="ef0cc-125">**Wyrażenie** — atrybut target hello jest wypełniana na podstawie wyniku hello wyrażenia przypominającej skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="ef0cc-126">Aby uzyskać więcej informacji, zobacz [pisać wyrażenia potrzeby mapowań atrybutów w usłudze Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="ef0cc-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="ef0cc-127">**Brak** — atrybut target hello zostanie pozostawiony bez modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="ef0cc-128">Jednak jeśli atrybut target hello jest kiedykolwiek puste, zostanie wprowadzony z wartością domyślną hello, który określisz.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="ef0cc-129">Dodanie toothese cztery podstawowe atrybutu mapowania typów mapowania atrybutu niestandardowego obsługuje pojęcie hello opcjonalny **domyślne** przypisanie wartości.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="ef0cc-130">Przypisanie wartości domyślne Hello gwarantuje, że atrybut docelowy jest wypełniana wartości, które nie istnieje żadna wartość w usłudze Azure AD, ani na obiekcie docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="ef0cc-131">najbardziej typowe konfiguracje Hello jest tooleave tym puste.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="ef0cc-132">Opis właściwości Mapowanie atrybutów</span><span class="sxs-lookup"><span data-stu-id="ef0cc-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="ef0cc-133">W poprzedniej sekcji hello zostały już wprowadzone toohello atrybutu mapowania typu właściwości.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="ef0cc-134">We właściwości toothis dodanie mapowań atrybutów obsługują hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ef0cc-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="ef0cc-135">**Atrybut źródłowy** -hello atrybut użytkownika z systemu źródłowego hello (np.: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ef0cc-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="ef0cc-136">**Atrybut TARGET** — Witaj atrybut użytkownika w systemie docelowym hello (np.: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="ef0cc-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="ef0cc-137">**Zgodne obiektów przy użyciu tego atrybutu** — czy stosuje się to mapowanie toouniquely zidentyfikować użytkowników między systemami hello źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="ef0cc-138">To jest zwykle ustawiana na powitania userPrincipalName lub atrybut poczty w usłudze Azure AD, która jest zwykle mapowane tooa pole nazwy użytkownika w aplikacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="ef0cc-139">**Dopasowywanie pierwszeństwo** — wiele pasujących atrybuty można ustawić.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="ef0cc-140">Jeśli dostępnych jest wiele, są oceniane pod w kolejności hello wynika z tego pola.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="ef0cc-141">Jak dopasowania zostanie znaleziony, żadne dodatkowe dopasowania atrybuty są oceniane.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="ef0cc-142">**Zastosuj to mapowanie**</span><span class="sxs-lookup"><span data-stu-id="ef0cc-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="ef0cc-143">**Zawsze** — Zastosuj to mapowanie na obu Tworzenie użytkownika i aktualizowanie akcji</span><span class="sxs-lookup"><span data-stu-id="ef0cc-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="ef0cc-144">**Tylko podczas tworzenia** -Zastosuj to mapowanie tylko akcje creation użytkownika</span><span class="sxs-lookup"><span data-stu-id="ef0cc-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="ef0cc-145">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="ef0cc-145">What you should know</span></span>

<span data-ttu-id="ef0cc-146">Microsoft Azure AD zapewnia wydajne wykonania procesu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="ef0cc-147">W środowisku zainicjowana tylko obiekty wymagające aktualizacji są przetwarzane podczas cyklu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="ef0cc-148">Aktualizowanie mapowań atrybutów ma wpływ na wydajność hello cyklu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="ef0cc-149">Konfiguracja mapowania atrybutu toohello aktualizacji wymaga wszystkich toobe zarządzanych obiektów ponownie oceniane.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="ef0cc-150">Jest zalecane najlepsze praktyki tookeep hello wiele mapowań atrybutów tooyour kolejne zmiany w co najmniej.</span><span class="sxs-lookup"><span data-stu-id="ef0cc-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef0cc-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef0cc-151">Next steps</span></span>

* [<span data-ttu-id="ef0cc-152">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef0cc-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ef0cc-153">Automatyzowanie inicjowania obsługi administracyjnej użytkowników/anulowania zastrzeżenia tooSaaS aplikacji</span><span class="sxs-lookup"><span data-stu-id="ef0cc-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="ef0cc-154">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="ef0cc-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="ef0cc-155">Filtry zakresu dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="ef0cc-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="ef0cc-156">Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="ef0cc-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="ef0cc-157">Powiadomienia aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="ef0cc-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="ef0cc-158">Lista samouczków dotyczących tooIntegrate aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="ef0cc-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

