---
title: "aaaUnexpected aplikacji na liście aplikacji | Dokumentacja firmy Microsoft"
description: "Jak toosee wszystkich aplikacji w dzierżawie i zrozumieć, jak aplikacje pojawiają się na liście wszystkie aplikacje w aplikacjach dla przedsiębiorstw"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="b388c-103">Nieoczekiwany aplikacji na liście aplikacji</span><span class="sxs-lookup"><span data-stu-id="b388c-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="b388c-104">W tym artykule pomocy toounderstand jak aplikacje pojawiają się w sieci **wszystkie aplikacje** w obszarze **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b388c-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="b388c-105">Jak toosee wszystkich aplikacji w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="b388c-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="b388c-106">toosee hello wszystkich aplikacji w dzierżawie, należy toouse hello **filtru** kontroli tooshow **wszystkie aplikacje** w obszarze hello **wszystkie aplikacje** listy.</span><span class="sxs-lookup"><span data-stu-id="b388c-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="b388c-107">toodo, wykonaj hello czynności:</span><span class="sxs-lookup"><span data-stu-id="b388c-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="b388c-108">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="b388c-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b388c-109">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="b388c-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b388c-110">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b388c-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b388c-111">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b388c-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b388c-112">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b388c-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="b388c-113">Kliknij przycisk hello Użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b388c-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="b388c-114">Na powitania **filtru** bloku, zestaw hello **Pokaż** opcję zbyt**wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="b388c-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="b388c-115">Dlaczego określonej aplikacji jest wyświetlany na liście wszystkie aplikacje</span><span class="sxs-lookup"><span data-stu-id="b388c-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="b388c-116">Gdy filtrowane zbyt**wszystkie aplikacje**, hello **wszystkie aplikacje** **listy** przedstawiono każdy obiekt nazwy głównej usługi w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b388c-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="b388c-117">Obiekty nazwy głównej usługi mogą być wyświetlane na liście na różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="b388c-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="b388c-118">Po dodaniu dowolną aplikację z galerii aplikacji hello, w tym:</span><span class="sxs-lookup"><span data-stu-id="b388c-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="b388c-119">**Azure AD galerii aplikacji** — aplikację, która została wstępnie zintegrowanych dla rejestracji jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b388c-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="b388c-120">**Aplikacje serwera Proxy aplikacji** — aplikacji działających w środowisku lokalnym, które mają tooprovide bezpiecznego jednokrotnego tooexternally.</span><span class="sxs-lookup"><span data-stu-id="b388c-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="b388c-121">**Niestandardowe opracowanych aplikacji** — aplikacji, który organizacja chce toodevelop na hello platformę tworzenia aplikacji w usłudze Azure AD, ale który nie istnieje jeszcze.</span><span class="sxs-lookup"><span data-stu-id="b388c-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="b388c-122">**Aplikacje inne niż galerii** — Przenoszenie własnych aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b388c-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="b388c-123">Wszelkie link sieci web, które mają lub dowolnej aplikacji, która renderuje pole nazwy użytkownika i hasła, obsługuje protokoły SAML lub OpenID Connect lub obsługuje SCIM, który ma toointegrate dla rejestracji jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b388c-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="b388c-124">Gdy skorzystania lub zalogowaniu się do 3<sup>usług pulpitu zdalnego</sup> aplikacji zintegrowany z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b388c-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="b388c-125">Przykładem tego jest [Smartsheet](https://app.smartsheet.com/b/home) lub [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="b388c-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="b388c-126">Gdy skorzystania lub dodanie tooa licencji użytkownika lub grupy tooa pierwszej strony aplikacji, takich jak [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="b388c-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="b388c-127">Po dodaniu nowej rejestracji aplikacji przez tworzenie aplikacji utworzonych niestandardowych za pomocą hello [rejestru aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="b388c-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="b388c-128">Po dodaniu nowej rejestracji aplikacji przez tworzenie aplikacji utworzonych niestandardowych za pomocą hello [portalu rejestracji aplikacji w wersji 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="b388c-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="b388c-129">Po dodaniu aplikacji tworzony jest przy użyciu programu Visual Studio [metod uwierzytelniania ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) lub [usług połączonych](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span><span class="sxs-lookup"><span data-stu-id="b388c-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="b388c-130">Podczas tworzenia obiektu główną usługi za pomocą hello [modułu Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="b388c-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="b388c-131">Gdy zostanie [zgody tooan aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) jako dane toouse administratorem w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b388c-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="b388c-132">Gdy [użytkownik zgadza aplikacji tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse danych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b388c-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="b388c-133">Po włączeniu pewnych usług, które przechowują dane w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b388c-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="b388c-134">Przykładem jest resetowania hasła, która ma formę jako toostore główna usługi resetowania hasła zasad bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="b388c-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="b388c-135">Przeczytaj więcej szczegółów, w jaki aplikacje są dodawane katalogu tooyour tooget [jak i dlaczego aplikacje są dodawane tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="b388c-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="b388c-136">Chcę tooremove określonego użytkownika lub grupy aplikacji tooan przypisania</span><span class="sxs-lookup"><span data-stu-id="b388c-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="b388c-137">tooremove użytkownika lub grupę przypisania tooan aplikację, wykonaj kroki hello na liście hello [Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b388c-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="b388c-138">Chcę toodisable wszystkich aplikacji tooan dostępu dla każdego użytkownika</span><span class="sxs-lookup"><span data-stu-id="b388c-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="b388c-139">toodisable wszystkie użytkownika logowania tooan aplikacji, wykonaj kroki hello na liście hello [wyłączyć logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b388c-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="b388c-140">Chcę całkowicie toodelete aplikacji</span><span class="sxs-lookup"><span data-stu-id="b388c-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="b388c-141">zbyt**usunąć aplikację**, postępuj zgodnie z poniższymi instrukcjami hello:</span><span class="sxs-lookup"><span data-stu-id="b388c-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="b388c-142">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="b388c-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b388c-143">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="b388c-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b388c-144">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b388c-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b388c-145">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b388c-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b388c-146">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b388c-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b388c-147">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="b388c-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b388c-148">Wybierz aplikację hello ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="b388c-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="b388c-149">Po załadowaniu aplikacji hello, kliknij przycisk **usunąć** ikony z aplikacji top hello **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="b388c-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="b388c-150">Chcę toodisable wszystkie przyszłe użytkownika zgody operacji tooany aplikacji</span><span class="sxs-lookup"><span data-stu-id="b388c-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="b388c-151">Wyłączanie zgody użytkownika dla użytkowników końcowych z aplikacji tooany zgodę zapobiec całego katalogu.</span><span class="sxs-lookup"><span data-stu-id="b388c-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="b388c-152">Administratorzy mogą nadal oznacza zgodę na behalves użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b388c-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="b388c-153">zgoda toolearn więcej informacji na temat aplikacji, oraz dlaczego może lub nie możesz toodo tego odczytu [zgody administratora i użytkownika opis](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="b388c-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="b388c-154">zbyt**Wyłącz wszystkie operacje zgody użytkownika w przyszłości w katalogu cały**, postępuj zgodnie z poniższymi instrukcjami hello:</span><span class="sxs-lookup"><span data-stu-id="b388c-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="b388c-155">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="b388c-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b388c-156">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="b388c-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b388c-157">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b388c-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b388c-158">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="b388c-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="b388c-159">Kliknij przycisk **ustawienia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b388c-159">click **User settings**.</span></span>

6.  <span data-ttu-id="b388c-160">Wyłącz wszystkie operacje zgody użytkownika w przyszłości przez ustawienie hello **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b388c-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b388c-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b388c-161">Next steps</span></span>
[<span data-ttu-id="b388c-162">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b388c-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
