---
title: 'Samouczek: Integracji Azure Active Directory z LinkedInSalesNavigator | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="6bf2e-103">Samouczek: Integracji Azure Active Directory z Nawigatora sprzedaży LinkedIn</span><span class="sxs-lookup"><span data-stu-id="6bf2e-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="6bf2e-104">Z tego samouczka dowiesz integrowanie Navigator sprzedaży LinkedIn z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6bf2e-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6bf2e-105">Integrowanie Navigator sprzedaży LinkedIn z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6bf2e-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6bf2e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do LinkedIn Nawigatora sprzedaży</span><span class="sxs-lookup"><span data-stu-id="6bf2e-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="6bf2e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do LinkedIn Nawigatora sprzedaży (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bf2e-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6bf2e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6bf2e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6bf2e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, Przeglądaj [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6bf2e-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bf2e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6bf2e-110">Prerequisites</span></span>

<span data-ttu-id="6bf2e-111">Do konfigurowania integracji z usługą Azure AD z LinkedIn Nawigator sprzedaży, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6bf2e-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="6bf2e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bf2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6bf2e-113">Nawigator sprzedaży LinkedIn jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6bf2e-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6bf2e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6bf2e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6bf2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6bf2e-116">Unikaj używania środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6bf2e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bf2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6bf2e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6bf2e-118">Scenario description</span></span>
<span data-ttu-id="6bf2e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6bf2e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6bf2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6bf2e-121">Dodawanie Navigator sprzedaży LinkedIn z galerii</span><span class="sxs-lookup"><span data-stu-id="6bf2e-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="6bf2e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6bf2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="6bf2e-123">Dodawanie Navigator sprzedaży LinkedIn z galerii</span><span class="sxs-lookup"><span data-stu-id="6bf2e-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="6bf2e-124">Aby skonfigurować integrację usługi Azure AD LinkedIn Nawigator sprzedaży, należy dodać Navigator sprzedaży LinkedIn z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6bf2e-125">**Aby dodać Navigator sprzedaży LinkedIn z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6bf2e-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6bf2e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6bf2e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6bf2e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6bf2e-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6bf2e-133">W polu wyszukiwania wpisz **LinkedIn sprzedaży Navigator**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="6bf2e-135">W panelu wyników wybierz **Nawigator sprzedaży LinkedIn**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6bf2e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6bf2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6bf2e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn Nawigator sprzedaży w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6bf2e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Nawigatorze sprzedaży LinkedIn jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="6bf2e-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Nawigatorze sprzedaży LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="6bf2e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Nawigatorze sprzedaży LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="6bf2e-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z LinkedIn Nawigator sprzedaży, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6bf2e-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6bf2e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6bf2e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6bf2e-145">**[Tworzenie użytkownika testowego Navigator sprzedaży LinkedIn](#creating-a-linkedin-sales-navigator-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LinkedIn Nawigator sprzedaży, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="6bf2e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6bf2e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6bf2e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6bf2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6bf2e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji LinkedIn sprzedaży nawigatora.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="6bf2e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LinkedIn Nawigator sprzedaży, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6bf2e-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="6bf2e-151">W portalu Azure na **Nawigator sprzedaży LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6bf2e-153">Na **logowanie jednokrotne** okna dialogowego, w **tryb** wybierz **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="6bf2e-155">W oknie przeglądarki sieci web inną logowania jednokrotnego w sieci **LinkedIn sprzedaży Nawigatora** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="6bf2e-156">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="6bf2e-157">Zaznacz również **Nawigator sprzedaży** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="6bf2e-159">Kliknij przycisk **lub kliknij tutaj, aby załadować i skopiuj poszczególnych pól w formularzu** i skopiuj **identyfikator jednostki** i **potwierdzenia konsumenta dostępu (ACS) adres Url**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="6bf2e-161">W portalu Azure w obszarze **LinkedIn sprzedaży Navigator domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="6bf2e-163">a.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-163">a.</span></span> <span data-ttu-id="6bf2e-164">W **identyfikator** pole tekstowe, wprowadź **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="6bf2e-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="6bf2e-165">b.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-165">b.</span></span> <span data-ttu-id="6bf2e-166">W **adres URL odpowiedzi** pole tekstowe, wprowadź **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="6bf2e-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="6bf2e-167">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="6bf2e-169">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="6bf2e-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="6bf2e-170">Twoje **LinkedIn sprzedaży Navigator** aplikacji oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="6bf2e-171">Poniższy zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-171">The following screenshot shows an example.</span></span> <span data-ttu-id="6bf2e-172">Wartość domyślna **identyfikator użytkownika** jest **user.userprincipalname** , ale Nawigator sprzedaży LinkedIn oczekuje być mapowane z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="6bf2e-173">Można użyć **user.mail** atrybutu z listy lub użyj wartości atrybutu odpowiednie na podstawie konfiguracji organizacji.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="6bf2e-175">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustawić atrybutów.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="6bf2e-176">Użytkownik chce dodać cztery oświadczeń o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość ma być zmapowana z **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio</span><span class="sxs-lookup"><span data-stu-id="6bf2e-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="6bf2e-177">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="6bf2e-177">Attribute Name</span></span> | <span data-ttu-id="6bf2e-178">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="6bf2e-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="6bf2e-179">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="6bf2e-179">email</span></span>| <span data-ttu-id="6bf2e-180">User.mail</span><span class="sxs-lookup"><span data-stu-id="6bf2e-180">user.mail</span></span> |
    | <span data-ttu-id="6bf2e-181">Dział</span><span class="sxs-lookup"><span data-stu-id="6bf2e-181">department</span></span>| <span data-ttu-id="6bf2e-182">User.Department</span><span class="sxs-lookup"><span data-stu-id="6bf2e-182">user.department</span></span> |
    | <span data-ttu-id="6bf2e-183">Imię</span><span class="sxs-lookup"><span data-stu-id="6bf2e-183">firstname</span></span>| <span data-ttu-id="6bf2e-184">User.givenName</span><span class="sxs-lookup"><span data-stu-id="6bf2e-184">user.givenname</span></span> |
    | <span data-ttu-id="6bf2e-185">nazwisko</span><span class="sxs-lookup"><span data-stu-id="6bf2e-185">lastname</span></span>| <span data-ttu-id="6bf2e-186">User.surname</span><span class="sxs-lookup"><span data-stu-id="6bf2e-186">user.surname</span></span> |
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="6bf2e-188">a.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-188">a.</span></span> <span data-ttu-id="6bf2e-189">Polecenie **Dodawanie atrybutu** aby otworzyć okno dialogowe atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="6bf2e-192">b.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-192">b.</span></span> <span data-ttu-id="6bf2e-193">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="6bf2e-194">c.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-194">c.</span></span> <span data-ttu-id="6bf2e-195">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6bf2e-196">d.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-196">d.</span></span> <span data-ttu-id="6bf2e-197">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="6bf2e-197">Click **Ok**</span></span>

10. <span data-ttu-id="6bf2e-198">Wykonaj następujące czynności na **nazwa** — atrybut</span><span class="sxs-lookup"><span data-stu-id="6bf2e-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="6bf2e-199">a.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-199">a.</span></span> <span data-ttu-id="6bf2e-200">Kliknij ten atrybut można otworzyć **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="6bf2e-202">b.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-202">b.</span></span> <span data-ttu-id="6bf2e-203">Usuń wartość adresu URL z **przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="6bf2e-204">c.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-204">c.</span></span> <span data-ttu-id="6bf2e-205">Kliknij przycisk **Ok** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="6bf2e-206">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="6bf2e-208">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-208">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="6bf2e-210">Przejdź do **ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="6bf2e-211">Kliknij przycisk **pliku XML, Przekaż** można przekazać pliku XML metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="6bf2e-213">Kliknij przycisk **na** do włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="6bf2e-214">Zmiany stanu rejestracji Jednokrotnej z **niepołączone** do **połączony**</span><span class="sxs-lookup"><span data-stu-id="6bf2e-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="6bf2e-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6bf2e-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6bf2e-217">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6bf2e-218">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6bf2e-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6bf2e-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bf2e-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="6bf2e-220">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6bf2e-222">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6bf2e-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6bf2e-223">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6bf2e-225">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6bf2e-227">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6bf2e-229">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6bf2e-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6bf2e-231">a.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-231">a.</span></span> <span data-ttu-id="6bf2e-232">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6bf2e-233">b.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-233">b.</span></span> <span data-ttu-id="6bf2e-234">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6bf2e-235">c.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-235">c.</span></span> <span data-ttu-id="6bf2e-236">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6bf2e-237">d.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-237">d.</span></span> <span data-ttu-id="6bf2e-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="6bf2e-239">Tworzenie użytkownika testowego LinkedIn Nawigator sprzedaży</span><span class="sxs-lookup"><span data-stu-id="6bf2e-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="6bf2e-240">Połączonej aplikacji Navigator sprzedaży obsługuje tylko w czasie (JIT) Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="6bf2e-241">Aktywuj **automatycznie przypisać licencje** przypisać licencję do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6bf2e-243">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bf2e-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6bf2e-244">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do LinkedIn sprzedaży nawigatora.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6bf2e-246">**Aby przypisać Simona Britta LinkedIn Nawigator sprzedaży, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6bf2e-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="6bf2e-247">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6bf2e-249">Na liście aplikacji zaznacz **LinkedIn sprzedaży Navigator**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="6bf2e-251">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6bf2e-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-253">Click **Add** button.</span></span> <span data-ttu-id="6bf2e-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6bf2e-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6bf2e-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6bf2e-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6bf2e-259">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6bf2e-259">Testing single sign-on</span></span>

<span data-ttu-id="6bf2e-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6bf2e-261">Po kliknięciu kafelka LinkedIn Nawigator sprzedaży w panelu dostępu, powinien być przekierowany do strony organizacji, gdzie należy podać informacje osobowe konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="6bf2e-262">Łączy konto osobiste konta firmowego LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bf2e-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="6bf2e-263">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="6bf2e-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6bf2e-264">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6bf2e-264">Additional resources</span></span>

* [<span data-ttu-id="6bf2e-265">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bf2e-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6bf2e-266">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6bf2e-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

