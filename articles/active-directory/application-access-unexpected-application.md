---
title: "Nieoczekiwany aplikacji na liście aplikacji | Dokumentacja firmy Microsoft"
description: "Jak wyświetlić wszystkie aplikacje w dzierżawie i zrozumieć, jak aplikacje pojawiają się na liście wszystkie aplikacje w aplikacjach dla przedsiębiorstw"
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="5d5af-103">Nieoczekiwany aplikacji na liście aplikacji</span><span class="sxs-lookup"><span data-stu-id="5d5af-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="5d5af-104">Ten artykuł ułatwia zrozumienie, jak aplikacje pojawiają się w sieci **wszystkie aplikacje** w obszarze **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5d5af-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="5d5af-105">Jak sprawdzić wszystkie aplikacje w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="5d5af-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="5d5af-106">Aby wyświetlić wszystkie aplikacje w dzierżawie, należy użyć **filtru** sterowania, aby wyświetlić **wszystkie aplikacje** w obszarze **wszystkie aplikacje** listy.</span><span class="sxs-lookup"><span data-stu-id="5d5af-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="5d5af-107">Aby to zrobić, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5d5af-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="5d5af-108">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="5d5af-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5d5af-109">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5d5af-110">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="5d5af-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5d5af-111">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d5af-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5d5af-112">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5d5af-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="5d5af-113">Kliknij opcję Użyj **filtru** kontroli nad **listę wszystkich aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5d5af-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="5d5af-114">Na **filtru** ustawić bloku **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="5d5af-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="5d5af-115">Dlaczego określonej aplikacji jest wyświetlany na liście wszystkie aplikacje</span><span class="sxs-lookup"><span data-stu-id="5d5af-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="5d5af-116">Gdy filtrowane do **wszystkie aplikacje**, **wszystkie aplikacje** **listy** przedstawiono każdy obiekt nazwy głównej usługi w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="5d5af-117">Obiekty nazwy głównej usługi mogą być wyświetlane na liście na różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="5d5af-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="5d5af-118">Po dodaniu dowolnej aplikacji w galerii aplikacji, w tym:</span><span class="sxs-lookup"><span data-stu-id="5d5af-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="5d5af-119">**Azure AD galerii aplikacji** — aplikację, która została wstępnie zintegrowanych dla rejestracji jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5af-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="5d5af-120">**Aplikacje serwera Proxy aplikacji** — aplikacji działających w środowisku lokalnym, który chcesz zapewnić bezpieczne jednokrotnego do zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="5d5af-121">**Niestandardowe opracowanych aplikacji** — aplikacji, który organizacja chce tworzenie aplikacji na platformie rozwoju aplikacji Azure AD, ale który nie istnieje jeszcze.</span><span class="sxs-lookup"><span data-stu-id="5d5af-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="5d5af-122">**Aplikacje inne niż galerii** — Przenoszenie własnych aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5d5af-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="5d5af-123">Wszelkie link sieci web, które mają lub dowolnej aplikacji, która renderuje pole nazwy użytkownika i hasła, obsługuje protokoły SAML lub OpenID Connect lub obsługuje SCIM, który chcesz zintegrować dla rejestracji jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5af-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="5d5af-124">Gdy skorzystania lub zalogowaniu się do 3<sup>usług pulpitu zdalnego</sup> aplikacji zintegrowany z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d5af-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="5d5af-125">Przykładem tego jest [Smartsheet](https://app.smartsheet.com/b/home) lub [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d5af-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="5d5af-126">Gdy skorzystania lub dodawanie licencję do użytkownika lub grupy do pierwszej aplikacji firm, takich jak [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="5d5af-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="5d5af-127">Po dodaniu nowej rejestracji aplikacji, tworząc niestandardowe rozwinięte aplikacji przy użyciu [rejestru aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="5d5af-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="5d5af-128">Po dodaniu nowej rejestracji aplikacji, tworząc niestandardowe rozwinięte aplikacji przy użyciu [portalu rejestracji aplikacji w wersji 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="5d5af-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="5d5af-129">Po dodaniu aplikacji tworzony jest przy użyciu programu Visual Studio [metod uwierzytelniania ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) lub [usług połączonych](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d5af-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="5d5af-130">Po utworzeniu, obiekt główny usługi za pomocą [modułu Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="5d5af-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="5d5af-131">Gdy zostanie [wyrażenia zgody na aplikację](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) jako administrator, aby użyć danych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="5d5af-132">Gdy [użytkownik zgadza się na aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) wykorzystanie danych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="5d5af-133">Po włączeniu pewnych usług, które przechowują dane w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="5d5af-134">Przykładem tego jest resetowania hasła, która ma formę jako nazwy głównej usługi do przechowywania hasła zasady resetowania bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="5d5af-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="5d5af-135">Aby uzyskać więcej informacji na temat sposobu aplikacji są dodawane do katalogu, przeczytaj [metody i przyczyny dodawania aplikacji do usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="5d5af-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="5d5af-136">Usunąć przypisanie określonego użytkownika lub grupy do aplikacji</span><span class="sxs-lookup"><span data-stu-id="5d5af-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="5d5af-137">Aby usunąć przypisanie grupy do aplikacji lub użytkownika, wykonaj czynności opisane w [Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d5af-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="5d5af-138">Chcę wyłączyć dostęp do aplikacji dla każdego użytkownika</span><span class="sxs-lookup"><span data-stu-id="5d5af-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="5d5af-139">Aby wyłączyć wszystkie logowania użytkownika do aplikacji, wykonaj czynności opisane w [wyłączyć logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d5af-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="5d5af-140">Chcę, aby całkowicie usunąć aplikację</span><span class="sxs-lookup"><span data-stu-id="5d5af-140">I want to delete an application entirely</span></span>

<span data-ttu-id="5d5af-141">Aby **usunąć aplikację**, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="5d5af-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="5d5af-142">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="5d5af-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5d5af-143">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5d5af-144">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="5d5af-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5d5af-145">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d5af-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5d5af-146">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5d5af-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5d5af-147">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="5d5af-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5d5af-148">Wybierz aplikację, którą chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="5d5af-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="5d5af-149">Po załadowaniu aplikacji, kliknij przycisk **usunąć** ikony z najwyższym aplikacji **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="5d5af-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="5d5af-150">Chcę wyłączyć wszystkie operacje zgody przyszłych użytkownika do aplikacji</span><span class="sxs-lookup"><span data-stu-id="5d5af-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="5d5af-151">Wyłączanie zgody użytkownika dla całego katalogu uniemożliwić użytkownikom końcowym zgodę dowolnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5d5af-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="5d5af-152">Administratorzy mogą nadal oznacza zgodę na behalves użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5d5af-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="5d5af-153">Dowiedz się więcej o zgodę aplikacji i dlaczego może lub nie chcesz to zrobić, przeczytaj [zgody administratora i użytkownika opis](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="5d5af-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="5d5af-154">Aby **Wyłącz wszystkie operacje zgody użytkownika w przyszłości w katalogu cały**, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="5d5af-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="5d5af-155">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="5d5af-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5d5af-156">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5d5af-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5d5af-157">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="5d5af-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5d5af-158">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="5d5af-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5d5af-159">Kliknij przycisk **ustawienia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5d5af-159">click **User settings**.</span></span>

6.  <span data-ttu-id="5d5af-160">Wyłącz wszystkie operacje zgody użytkownika w przyszłości przez ustawienie **użytkownicy mogą zezwolić aplikacjom na dostęp do danych** Przełącz, aby **nr** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d5af-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d5af-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d5af-161">Next steps</span></span>
[<span data-ttu-id="5d5af-162">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d5af-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
