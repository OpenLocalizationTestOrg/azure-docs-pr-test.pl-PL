---
title: "aaaDevelop aplikacji dla usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Przeznaczone dla specjalistów IT hello, w tym artykule przedstawiono wskazówki dotyczące integracji aplikacji Azure z usługą Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="7ba05-103">Tworzenie aplikacji biznesowych z usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ba05-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="7ba05-104">Ten przewodnik zawiera omówienie programu biznesowych (LoB) aplikacji dla .hello Azure Active Directory (AD), przeznaczone odbiorców jest Administratorzy globalni usługi Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="7ba05-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="7ba05-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7ba05-105">Overview</span></span>
<span data-ttu-id="7ba05-106">Tworzenie aplikacji zintegrowanych z usługą Azure AD pozwala użytkownikom w Twojej organizacji logowanie jednokrotne z usługą Office 365.</span><span class="sxs-lookup"><span data-stu-id="7ba05-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="7ba05-107">Posiadanie aplikacji hello Azure AD pozwala kontrolować hello zasad uwierzytelniania dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7ba05-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="7ba05-108">więcej informacji na temat dostępu warunkowego i jak wyświetlić tooprotect aplikacji przy użyciu uwierzytelniania wieloskładnikowego (MFA) toolearn [Konfigurowanie reguł dostępu](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7ba05-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="7ba05-109">Zarejestruj toouse Twojej aplikacji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ba05-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="7ba05-110">Rejestrowanie aplikacji hello oznacza, że deweloperów można użytkownicy tooauthenticate usługi Azure AD i żądania dostępu toouser zasoby, takie jak wiadomości e-mail, kalendarza i dokumenty.</span><span class="sxs-lookup"><span data-stu-id="7ba05-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="7ba05-111">Każdy członek katalogu (nie gości) można zarejestrować aplikacji, nazywanego *tworzenia obiektu aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="7ba05-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="7ba05-112">Rejestrowanie aplikacji umożliwia skonfigurowanie następujących hello toodo dowolnego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="7ba05-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="7ba05-113">Uzyskać tożsamości dla swoich aplikacji, która rozpoznaje usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ba05-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="7ba05-114">Jeden lub więcej klucze tajne/kluczy, które hello aplikacji można skorzystaj tooauthenticate samego tooAD</span><span class="sxs-lookup"><span data-stu-id="7ba05-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="7ba05-115">Aplikacja hello marki w hello portalu Azure z niestandardowej nazwy, logo, itp.</span><span class="sxs-lookup"><span data-stu-id="7ba05-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="7ba05-116">Zastosuj aplikacji tootheir funkcje autoryzacji usługi Azure AD, w tym:</span><span class="sxs-lookup"><span data-stu-id="7ba05-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="7ba05-117">Kontrola dostępu oparta na rolach (RBAC)</span><span class="sxs-lookup"><span data-stu-id="7ba05-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="7ba05-118">Usługa Azure Active Directory jako serwera autoryzacji oAuth (interfejs API udostępnianych przez aplikacji hello bezpieczna)</span><span class="sxs-lookup"><span data-stu-id="7ba05-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="7ba05-119">Zadeklaruj wymaganych uprawnień niezbędnych do toofunction aplikacji hello zgodnie z oczekiwaniami, w tym:</span><span class="sxs-lookup"><span data-stu-id="7ba05-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="7ba05-120">Uprawnienia aplikacji (tylko administratorzy globalni).</span><span class="sxs-lookup"><span data-stu-id="7ba05-120">App permissions (global administrators only).</span></span> <span data-ttu-id="7ba05-121">Na przykład: rola członkostwa w innej usłudze Azure AD aplikacji lub roli członkostwa względną tooan Azure zasobu, grupy zasobów, lub subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7ba05-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="7ba05-122">Delegowane uprawnienia (każdy użytkownik).</span><span class="sxs-lookup"><span data-stu-id="7ba05-122">Delegated permissions (any user).</span></span> <span data-ttu-id="7ba05-123">Na przykład: usługi Azure AD, logowania i odczytu profilu</span><span class="sxs-lookup"><span data-stu-id="7ba05-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="7ba05-124">Domyślnie każdy członek można zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7ba05-124">By default, any member can register an application.</span></span> <span data-ttu-id="7ba05-125">toolearn toorestrict uprawnienia do rejestrowania aplikacji toospecific członków, zobacz temat [sposób dodawania aplikacji tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="7ba05-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="7ba05-126">Oto należy, administrator globalny hello, muszą toodo toohelp deweloperzy tworzą ich stosowania gotowa do produkcji:</span><span class="sxs-lookup"><span data-stu-id="7ba05-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="7ba05-127">Konfigurowanie reguł dostępu (zasady dostępu/MFA)</span><span class="sxs-lookup"><span data-stu-id="7ba05-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="7ba05-128">Konfigurowanie przypisanie użytkownika toorequire aplikacji hello i przypisywać użytkowników</span><span class="sxs-lookup"><span data-stu-id="7ba05-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="7ba05-129">Pomiń hello domyślne środowisko zgody użytkownika</span><span class="sxs-lookup"><span data-stu-id="7ba05-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="7ba05-130">Skonfiguruj reguły dostępu</span><span class="sxs-lookup"><span data-stu-id="7ba05-130">Configure access rules</span></span>
<span data-ttu-id="7ba05-131">Konfigurowanie aplikacji SaaS tooyour reguł dostępu dla poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7ba05-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="7ba05-132">Można na przykład wymagać uwierzytelniania MFA lub Zezwalaj toousers dostępu tylko w sieciach zaufanych.</span><span class="sxs-lookup"><span data-stu-id="7ba05-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="7ba05-133">Szczegóły Hello tego są dostępne w dokumencie hello [Konfigurowanie reguł dostępu](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7ba05-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="7ba05-134">Konfigurowanie przypisanie użytkownika toorequire aplikacji hello i przypisywać użytkowników</span><span class="sxs-lookup"><span data-stu-id="7ba05-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="7ba05-135">Domyślnie użytkownicy mogą uzyskiwać dostęp do aplikacji bez przypisywane.</span><span class="sxs-lookup"><span data-stu-id="7ba05-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="7ba05-136">Jednak aplikacja hello przedstawia role lub ma tooappear aplikacji hello na panelu dostępu użytkownika, należy włączyć przypisanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7ba05-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

<span data-ttu-id="7ba05-137">[Requiring user assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) (Wymaganie przypisania użytkownika)</span><span class="sxs-lookup"><span data-stu-id="7ba05-137">[Requiring user assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md)</span></span>

<span data-ttu-id="7ba05-138">Jeśli jesteś subskrybentem Azure AD Premium lub Enterprise Mobility Suite (EMS), zdecydowanie zaleca się korzystanie z grup.</span><span class="sxs-lookup"><span data-stu-id="7ba05-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="7ba05-139">Przypisywanie grup aplikacji toohello umożliwia toodelegate trwającą dostępu administracyjnego toohello właściciela grupy hello.</span><span class="sxs-lookup"><span data-stu-id="7ba05-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="7ba05-140">Można utworzyć grupy hello lub poprosić stronę odpowiedzialny hello w grupie hello toocreate organizacji przy użyciu funkcji z grupy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="7ba05-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="7ba05-141">Przypisywanie użytkowników tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="7ba05-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="7ba05-142">Przypisywanie grup aplikacji tooan</span><span class="sxs-lookup"><span data-stu-id="7ba05-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="7ba05-143">Pomiń zgody użytkownika</span><span class="sxs-lookup"><span data-stu-id="7ba05-143">Suppress user consent</span></span>
<span data-ttu-id="7ba05-144">Domyślnie każdy użytkownik przechodzi przez toosign środowisko zgody w.</span><span class="sxs-lookup"><span data-stu-id="7ba05-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="7ba05-145">środowisko zgody Hello, prosząc użytkowników toogrant uprawnienia aplikacji tooan może być niejasna dla użytkowników, którzy nie zna podejmowanie tych decyzji.</span><span class="sxs-lookup"><span data-stu-id="7ba05-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="7ba05-146">Dla aplikacji, którym ufasz można uprościć czynności użytkownika hello przez aplikację toohello zgodę imieniu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="7ba05-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="7ba05-147">Aby uzyskać więcej informacji o zgodę użytkownika i zgody hello uruchomienia na platformie Azure, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7ba05-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="7ba05-148">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="7ba05-148">Related Articles</span></span>
* [<span data-ttu-id="7ba05-149">Włączanie aplikacji lokalnych tooon bezpieczny dostęp zdalny za pomocą serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ba05-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="7ba05-150">Podgląd warunkowego dostępu na platformie Azure dla aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="7ba05-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="7ba05-151">Zarządzanie tooapps dostępu w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ba05-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="7ba05-152">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ba05-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
