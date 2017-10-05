---
title: 'Samouczek: Integracji Azure Active Directory z wyszukiwania LinkedIn | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LinkedIn wyszukiwania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="0ece9-103">Samouczek: Integracji Azure Active Directory z LinkedIn wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0ece9-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="0ece9-104">W tym samouczku Dowiedz się jak integracji LinkedIn wyszukiwania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ece9-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ece9-105">Integrowanie wyszukiwania LinkedIn z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0ece9-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0ece9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do wyszukiwania LinkedIn</span><span class="sxs-lookup"><span data-stu-id="0ece9-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="0ece9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do wyszukiwania LinkedIn (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ece9-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ece9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ece9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0ece9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ece9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ece9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0ece9-110">Prerequisites</span></span>

<span data-ttu-id="0ece9-111">Aby skonfigurować integrację usługi Azure AD z LinkedIn wyszukiwania, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0ece9-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="0ece9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ece9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ece9-113">Wyszukiwanie LinkedIn jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0ece9-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ece9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ece9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0ece9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ece9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0ece9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ece9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ece9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ece9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0ece9-118">Scenario description</span></span>
<span data-ttu-id="0ece9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0ece9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ece9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0ece9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ece9-121">Dodawanie wyszukiwania LinkedIn z galerii</span><span class="sxs-lookup"><span data-stu-id="0ece9-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="0ece9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0ece9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="0ece9-123">Dodawanie wyszukiwania LinkedIn z galerii</span><span class="sxs-lookup"><span data-stu-id="0ece9-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="0ece9-124">Aby skonfigurować integrację LinkedIn wyszukiwania w usłudze Azure Active Directory, należy dodać wyszukiwania LinkedIn z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0ece9-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ece9-125">**Aby dodać wyszukiwania LinkedIn z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0ece9-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0ece9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0ece9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0ece9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0ece9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0ece9-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego, aby dodać nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="0ece9-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0ece9-133">W polu wyszukiwania wpisz **wyszukiwania LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="0ece9-135">W panelu wyników wybierz **wyszukiwania LinkedIn**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="0ece9-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ece9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0ece9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ece9-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ece9-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednikiem LinkedIn odnośnika do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ece9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="0ece9-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w wyszukiwaniu LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0ece9-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="0ece9-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** odnośnika LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0ece9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="0ece9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="0ece9-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0ece9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0ece9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0ece9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0ece9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ece9-145">**[Tworzenie użytkownika testowego wyszukiwania LinkedIn](#creating-an-linkedin-lookup-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LinkedIn wyszukiwania, które jest połączone z reprezentacją usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ece9-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="0ece9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0ece9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ece9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="0ece9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0ece9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0ece9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0ece9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji wyszukiwania LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0ece9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="0ece9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0ece9-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="0ece9-151">W portalu Azure na **wyszukiwania LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0ece9-153">Na **logowanie jednokrotne** okna dialogowego, w **tryb** wybierz **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="0ece9-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="0ece9-155">W oknie przeglądarki sieci web inną logowania jednokrotnego w sieci **wyszukiwania LinkedIn** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0ece9-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="0ece9-156">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="0ece9-157">Zaznacz również **wyszukiwania** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="0ece9-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="0ece9-159">Kliknij przycisk **lub kliknij tutaj, aby załadować i skopiuj poszczególnych pól w formularzu** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**</span><span class="sxs-lookup"><span data-stu-id="0ece9-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="0ece9-161">W portalu Azure w obszarze **domeny wyszukiwania LinkedIn i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="0ece9-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="0ece9-163">a.</span><span class="sxs-lookup"><span data-stu-id="0ece9-163">a.</span></span> <span data-ttu-id="0ece9-164">W **identyfikator** pole tekstowe, wprowadź **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="0ece9-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="0ece9-165">b.</span><span class="sxs-lookup"><span data-stu-id="0ece9-165">b.</span></span> <span data-ttu-id="0ece9-166">W **adres URL odpowiedzi** pole tekstowe, wprowadź **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="0ece9-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="0ece9-167">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="0ece9-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="0ece9-169">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="0ece9-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0ece9-170">To nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="0ece9-170">This is not real value.</span></span> <span data-ttu-id="0ece9-171">Użytkownik musi zaktualizować te wartości z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="0ece9-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="0ece9-172">Skontaktuj się z [zespołem pomocy technicznej klienta wyszukiwania LinkedIn](https://business.LinkedIn.com/lookup) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="0ece9-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="0ece9-173">Twoje **wyszukiwania LinkedIn** aplikacji oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="0ece9-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0ece9-174">Użytkownik ma dodanie mapowań atrybutów niestandardowych do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="0ece9-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="0ece9-175">Poniższy zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="0ece9-175">The following screenshot shows an example.</span></span> <span data-ttu-id="0ece9-176">Wartość domyślna **identyfikator użytkownika** jest **user.userprincipalname** , ale wyszukiwania LinkedIn oczekuje to być mapowane z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ece9-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="0ece9-177">Można użyć **user.mail** atrybutu z listy lub użyj wartości atrybutu odpowiednie na podstawie konfiguracji organizacji.</span><span class="sxs-lookup"><span data-stu-id="0ece9-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="0ece9-179">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustawić atrybutów.</span><span class="sxs-lookup"><span data-stu-id="0ece9-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="0ece9-180">Użytkownik chce dodać cztery oświadczeń o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość ma być zmapowana z **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio</span><span class="sxs-lookup"><span data-stu-id="0ece9-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="0ece9-181">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="0ece9-181">Attribute Name</span></span> | <span data-ttu-id="0ece9-182">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="0ece9-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0ece9-183">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="0ece9-183">email</span></span>| <span data-ttu-id="0ece9-184">User.mail</span><span class="sxs-lookup"><span data-stu-id="0ece9-184">user.mail</span></span> |    
    | <span data-ttu-id="0ece9-185">Dział</span><span class="sxs-lookup"><span data-stu-id="0ece9-185">department</span></span>| <span data-ttu-id="0ece9-186">User.Department</span><span class="sxs-lookup"><span data-stu-id="0ece9-186">user.department</span></span> |
    | <span data-ttu-id="0ece9-187">Imię</span><span class="sxs-lookup"><span data-stu-id="0ece9-187">firstname</span></span>| <span data-ttu-id="0ece9-188">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0ece9-188">user.givenname</span></span> |
    | <span data-ttu-id="0ece9-189">nazwisko</span><span class="sxs-lookup"><span data-stu-id="0ece9-189">lastname</span></span>| <span data-ttu-id="0ece9-190">User.surname</span><span class="sxs-lookup"><span data-stu-id="0ece9-190">user.surname</span></span> |

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="0ece9-192">a.</span><span class="sxs-lookup"><span data-stu-id="0ece9-192">a.</span></span> <span data-ttu-id="0ece9-193">Kliknij przycisk **Dodawanie atrybutu** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="0ece9-196">b.</span><span class="sxs-lookup"><span data-stu-id="0ece9-196">b.</span></span> <span data-ttu-id="0ece9-197">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="0ece9-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0ece9-198">c.</span><span class="sxs-lookup"><span data-stu-id="0ece9-198">c.</span></span> <span data-ttu-id="0ece9-199">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="0ece9-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0ece9-200">d.</span><span class="sxs-lookup"><span data-stu-id="0ece9-200">d.</span></span> <span data-ttu-id="0ece9-201">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="0ece9-201">Click **Ok**</span></span>

10. <span data-ttu-id="0ece9-202">Wykonaj następujące czynności na **nazwa** — atrybut</span><span class="sxs-lookup"><span data-stu-id="0ece9-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="0ece9-203">a.</span><span class="sxs-lookup"><span data-stu-id="0ece9-203">a.</span></span> <span data-ttu-id="0ece9-204">Kliknij ten atrybut można otworzyć **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="0ece9-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="0ece9-206">b.</span><span class="sxs-lookup"><span data-stu-id="0ece9-206">b.</span></span> <span data-ttu-id="0ece9-207">Usuń wartość adresu URL z **przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="0ece9-208">c.</span><span class="sxs-lookup"><span data-stu-id="0ece9-208">c.</span></span> <span data-ttu-id="0ece9-209">Kliknij przycisk **Ok** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="0ece9-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="0ece9-210">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ece9-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="0ece9-212">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0ece9-212">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="0ece9-214">Przejdź do **ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="0ece9-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="0ece9-215">Przekaż plik XML został pobrany z portalu Azure, klikając **pliku XML, Przekaż** opcji.</span><span class="sxs-lookup"><span data-stu-id="0ece9-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="0ece9-217">Kliknij przycisk **na** do włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="0ece9-218">Zmiany stanu rejestracji Jednokrotnej z **niepołączone** do **połączony**</span><span class="sxs-lookup"><span data-stu-id="0ece9-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="0ece9-220">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="0ece9-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0ece9-221">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="0ece9-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0ece9-222">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ece9-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ece9-223">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ece9-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="0ece9-224">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0ece9-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0ece9-226">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0ece9-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0ece9-227">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0ece9-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ece9-229">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ece9-231">Kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ece9-233">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0ece9-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ece9-235">a.</span><span class="sxs-lookup"><span data-stu-id="0ece9-235">a.</span></span> <span data-ttu-id="0ece9-236">W **nazwa** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="0ece9-237">b.</span><span class="sxs-lookup"><span data-stu-id="0ece9-237">b.</span></span> <span data-ttu-id="0ece9-238">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0ece9-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="0ece9-239">c.</span><span class="sxs-lookup"><span data-stu-id="0ece9-239">c.</span></span> <span data-ttu-id="0ece9-240">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0ece9-241">d.</span><span class="sxs-lookup"><span data-stu-id="0ece9-241">d.</span></span> <span data-ttu-id="0ece9-242">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="0ece9-243">Tworzenie użytkownika testowego LinkedIn wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0ece9-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="0ece9-244">Połączonej aplikacji wyszukiwania obsługuje tylko w czasie (JIT) Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ece9-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="0ece9-245">Aktywuj **automatycznie przypisać licencje** przypisać licencję do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ece9-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0ece9-247">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ece9-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0ece9-248">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do wyszukiwania LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0ece9-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0ece9-250">**Aby przypisać Simona Britta LinkedIn wyszukiwania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0ece9-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="0ece9-251">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0ece9-253">Na liście aplikacji zaznacz **wyszukiwania LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="0ece9-255">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0ece9-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0ece9-257">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0ece9-257">Click **Add** button.</span></span> <span data-ttu-id="0ece9-258">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0ece9-260">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="0ece9-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0ece9-261">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ece9-262">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ece9-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0ece9-263">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0ece9-263">Testing single sign-on</span></span>

<span data-ttu-id="0ece9-264">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0ece9-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0ece9-265">Po kliknięciu kafelka LinkedIn wyszukiwania w panelu dostępu, powinien być przekierowany do strony organizacji, gdzie należy podać informacje osobowe konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0ece9-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="0ece9-266">Łączy konto osobiste konta firmowego LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0ece9-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="0ece9-267">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ece9-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0ece9-268">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0ece9-268">Additional resources</span></span>

* [<span data-ttu-id="0ece9-269">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ece9-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ece9-270">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ece9-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

