---
title: "Tworzenie aplikacji dla usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zapisane dla specjalistów IT, w tym artykule przedstawiono wskazówki dotyczące integracji aplikacji Azure z usługą Active Directory."
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="fa1c2-103">Tworzenie aplikacji biznesowych z usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa1c2-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="fa1c2-104">Ten przewodnik zawiera omówienie tworzenia — biznesowych (LoB) aplikacji dla usługi Azure Active Directory (AD). Docelowa grupa odbiorców jest Administratorzy globalni usługi Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="fa1c2-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fa1c2-105">Overview</span></span>
<span data-ttu-id="fa1c2-106">Tworzenie aplikacji zintegrowanych z usługą Azure AD pozwala użytkownikom w Twojej organizacji logowanie jednokrotne z usługą Office 365.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="fa1c2-107">W usłudze Azure AD umożliwia kontrolę nad zasady uwierzytelniania dla aplikacji, których aplikacja.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="fa1c2-108">Aby dowiedzieć się więcej na temat dostępu warunkowego i jak chronić aplikacje z uwierzytelnianiem wieloskładnikowym (MFA), zobacz [Konfigurowanie reguł dostępu](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fa1c2-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="fa1c2-109">Rejestrowanie aplikacji do użycia usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="fa1c2-110">Trwa rejestrowanie aplikacji oznacza, że deweloperów można używać usługi Azure AD do uwierzytelniania użytkowników i uzyskać dostęp do zasobów użytkownika, takie jak wiadomości e-mail, kalendarza i dokumentów.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="fa1c2-111">Każdy członek katalogu (nie gości) można zarejestrować aplikacji, nazywanego *tworzenia obiektu aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="fa1c2-112">Rejestrowanie aplikacji zezwala każdemu użytkownikowi wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fa1c2-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="fa1c2-113">Uzyskać tożsamości dla swoich aplikacji, która rozpoznaje usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa1c2-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="fa1c2-114">Pobierz co najmniej jeden haseł/kluczy używanych przez aplikację do samodzielnego uwierzytelnienia w usłudze AD</span><span class="sxs-lookup"><span data-stu-id="fa1c2-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="fa1c2-115">Marki aplikacji w portalu Azure z niestandardowej nazwy, logo, itp.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="fa1c2-116">Stosować funkcje autoryzacji usługi Azure AD do swoich aplikacji, w tym:</span><span class="sxs-lookup"><span data-stu-id="fa1c2-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="fa1c2-117">Kontrola dostępu oparta na rolach (RBAC)</span><span class="sxs-lookup"><span data-stu-id="fa1c2-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="fa1c2-118">Usługa Azure Active Directory jako serwera autoryzacji oAuth (bezpieczna udostępniany przez aplikację interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="fa1c2-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="fa1c2-119">Zadeklarować wymagane uprawnienia niezbędne do funkcji aplikacji zgodnie z oczekiwaniami, w tym:</span><span class="sxs-lookup"><span data-stu-id="fa1c2-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="fa1c2-120">Uprawnienia aplikacji (tylko administratorzy globalni).</span><span class="sxs-lookup"><span data-stu-id="fa1c2-120">App permissions (global administrators only).</span></span> <span data-ttu-id="fa1c2-121">Na przykład: członkostwo roli w innej usłudze Azure AD aplikacji lub członkostwa względem Azure zasobu, grupy zasobów, lub subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fa1c2-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="fa1c2-122">Delegowane uprawnienia (każdy użytkownik).</span><span class="sxs-lookup"><span data-stu-id="fa1c2-122">Delegated permissions (any user).</span></span> <span data-ttu-id="fa1c2-123">Na przykład: usługi Azure AD, logowania i odczytu profilu</span><span class="sxs-lookup"><span data-stu-id="fa1c2-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="fa1c2-124">Domyślnie każdy członek można zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-124">By default, any member can register an application.</span></span> <span data-ttu-id="fa1c2-125">Aby dowiedzieć się, jak ograniczyć uprawnienia do rejestrowania aplikacji do określonego członka, zobacz [jak aplikacje są dodawane do usługi Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="fa1c2-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="fa1c2-126">Oto, co, administrator globalny, należy wykonać, aby pomóc deweloperom przygotowania aplikacji do produkcji:</span><span class="sxs-lookup"><span data-stu-id="fa1c2-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="fa1c2-127">Konfigurowanie reguł dostępu (zasady dostępu/MFA)</span><span class="sxs-lookup"><span data-stu-id="fa1c2-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="fa1c2-128">Konfiguruje aplikację do wymagają przypisania użytkownika i Przypisz użytkowników</span><span class="sxs-lookup"><span data-stu-id="fa1c2-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="fa1c2-129">Pomiń domyślne środowisko zgody użytkownika</span><span class="sxs-lookup"><span data-stu-id="fa1c2-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="fa1c2-130">Skonfiguruj reguły dostępu</span><span class="sxs-lookup"><span data-stu-id="fa1c2-130">Configure access rules</span></span>
<span data-ttu-id="fa1c2-131">Konfigurowanie reguł dla poszczególnych aplikacji dostępu do aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="fa1c2-132">Można na przykład wymagać uwierzytelniania MFA lub tylko zezwolić na dostęp do użytkowników w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="fa1c2-133">Dla tego są one dostępne w dokumencie [Konfigurowanie reguł dostępu](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fa1c2-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="fa1c2-134">Konfiguruje aplikację do wymagają przypisania użytkownika i Przypisz użytkowników</span><span class="sxs-lookup"><span data-stu-id="fa1c2-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="fa1c2-135">Domyślnie użytkownicy mogą uzyskiwać dostęp do aplikacji bez przypisywane.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="fa1c2-136">Jednak aplikacja udostępnia ról lub chcesz aplikacji na panelu dostępu użytkownika, należy włączyć przypisanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

<span data-ttu-id="fa1c2-137">[Requiring user assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) (Wymaganie przypisania użytkownika)</span><span class="sxs-lookup"><span data-stu-id="fa1c2-137">[Requiring user assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md)</span></span>

<span data-ttu-id="fa1c2-138">Jeśli jesteś subskrybentem Azure AD Premium lub Enterprise Mobility Suite (EMS), zdecydowanie zaleca się korzystanie z grup.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="fa1c2-139">Przypisywanie grup do aplikacji umożliwia delegowanie zarządzania stałe dostępu do właściciela grupy.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="fa1c2-140">Można utworzyć grupy lub poprosić odpowiedzialny stronę w Twojej organizacji, aby utworzyć grupę przy użyciu funkcji z grupy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

<span data-ttu-id="fa1c2-141">[Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) (Przypisywanie użytkowników do aplikacji)</span><span class="sxs-lookup"><span data-stu-id="fa1c2-141">[Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md)</span></span>  
<span data-ttu-id="fa1c2-142">[Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md) (Przypisywanie grup do aplikacji)</span><span class="sxs-lookup"><span data-stu-id="fa1c2-142">[Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md)</span></span>

## <a name="suppress-user-consent"></a><span data-ttu-id="fa1c2-143">Pomiń zgody użytkownika</span><span class="sxs-lookup"><span data-stu-id="fa1c2-143">Suppress user consent</span></span>
<span data-ttu-id="fa1c2-144">Domyślnie każdy użytkownik przechodzi przez środowisko zgody, do logowania.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="fa1c2-145">Środowisko zgody, prosząc użytkowników można przyznać uprawnień do aplikacji, może być niejasna dla użytkowników, którzy nie zna podejmowanie tych decyzji.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="fa1c2-146">Dla aplikacji, którym ufasz można uprościć czynności użytkowników przez zgodę aplikacji w imieniu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="fa1c2-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="fa1c2-147">Aby uzyskać więcej informacji o zgodę użytkownika i zgody występują na platformie Azure, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="fa1c2-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="fa1c2-148">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="fa1c2-148">Related Articles</span></span>
* [<span data-ttu-id="fa1c2-149">Włącz bezpieczny dostęp zdalny do aplikacji lokalnych przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa1c2-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="fa1c2-150">Podgląd warunkowego dostępu na platformie Azure dla aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="fa1c2-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="fa1c2-151">Zarządzanie dostępem do aplikacji z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa1c2-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="fa1c2-152">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa1c2-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
