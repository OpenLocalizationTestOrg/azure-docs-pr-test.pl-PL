---
title: "Samouczek: Integracji Azure Active Directory z usług Salesforce | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="208d1-103">Samouczek: Integracji Azure Active Directory z usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="208d1-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="208d1-104">Z tego samouczka dowiesz się Integrowanie usługi Salesforce z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="208d1-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="208d1-105">Integrowanie usługi Salesforce z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="208d1-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="208d1-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="208d1-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="208d1-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do usług Salesforce (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="208d1-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="208d1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="208d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="208d1-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="208d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="208d1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="208d1-110">Prerequisites</span></span>

<span data-ttu-id="208d1-111">Aby skonfigurować integrację usługi Azure AD z usług Salesforce, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="208d1-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="208d1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="208d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="208d1-113">Salesforce jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="208d1-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="208d1-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="208d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="208d1-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="208d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="208d1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="208d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="208d1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="208d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="208d1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="208d1-118">Scenario description</span></span>
<span data-ttu-id="208d1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="208d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="208d1-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="208d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="208d1-121">Dodawanie usługi Salesforce z galerii</span><span class="sxs-lookup"><span data-stu-id="208d1-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="208d1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="208d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="208d1-123">Dodawanie usługi Salesforce z galerii</span><span class="sxs-lookup"><span data-stu-id="208d1-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="208d1-124">Aby skonfigurować integrację usługi Salesforce z usługą Azure AD, należy dodać usługi Salesforce z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="208d1-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="208d1-125">**Aby dodać usługi Salesforce z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="208d1-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="208d1-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="208d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="208d1-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="208d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="208d1-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="208d1-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="208d1-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="208d1-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="208d1-133">W polu wyszukiwania wpisz **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="208d1-133">In the search box, type **Salesforce**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="208d1-135">W panelu wyników wybierz **Salesforce**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="208d1-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="208d1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="208d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="208d1-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Salesforce na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="208d1-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="208d1-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w usłudze Salesforce jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="208d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="208d1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązane użytkownika w usłudze Salesforce musi określone.</span><span class="sxs-lookup"><span data-stu-id="208d1-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="208d1-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="208d1-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usług Salesforce, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="208d1-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="208d1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="208d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="208d1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="208d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="208d1-145">**[Tworzenie użytkownika testowego Salesforce](#creating-a-salesforce-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Salesforce połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="208d1-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="208d1-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="208d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="208d1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="208d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="208d1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="208d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="208d1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="208d1-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usług Salesforce, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="208d1-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="208d1-151">W portalu Azure na **Salesforce** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="208d1-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="208d1-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="208d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="208d1-155">Na **domeny Salesforce i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="208d1-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="208d1-157">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="208d1-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="208d1-158">Konto przedsiębiorstwa:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="208d1-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="208d1-159">Konta dewelopera:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="208d1-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="208d1-160">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="208d1-160">These values are not the real.</span></span> <span data-ttu-id="208d1-161">Adres URL logowania rzeczywiste, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="208d1-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="208d1-162">Skontaktuj się z [zespołem pomocy technicznej klienta usług Salesforce](https://help.salesforce.com/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="208d1-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="208d1-163">Na **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="208d1-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="208d1-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="208d1-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="208d1-167">Na **konfiguracji Salesforce** , kliknij przycisk **skonfigurować Salesforce** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="208d1-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="208d1-168">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="208d1-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="208d1-169">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="208d1-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="208d1-170">Otwórz nową kartę w przeglądarce i zaloguj się do konta administratora usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="208d1-171">W obszarze **administratora** okienka nawigacji kliknij **kontroli bezpieczeństwa** do rozwiń sekcję pokrewne.</span><span class="sxs-lookup"><span data-stu-id="208d1-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="208d1-172">Następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="208d1-172">Then click **Single Sign-On Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="208d1-174">Na **ustawień rejestracji jednokrotnej** kliknij przycisk **Edytuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="208d1-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="208d1-175">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="208d1-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="208d1-176">Jeśli nie można włączyć logowanie jednokrotne ustawień konta usług Salesforce, konieczne może być skontaktuj się z [zespołem pomocy technicznej klienta usług Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="208d1-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="208d1-177">Wybierz **włączone SAML**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="208d1-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="208d1-179">Aby skonfigurować SAML pojedynczego logowania jednokrotnego ustawienia, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="208d1-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="208d1-181">Na **SAML pojedynczego logowania jednokrotnego ustawienie Edytuj** strony, sprawdź następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="208d1-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="208d1-183">a.</span><span class="sxs-lookup"><span data-stu-id="208d1-183">a.</span></span> <span data-ttu-id="208d1-184">Aby uzyskać **nazwa** wpisz przyjazną nazwę dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="208d1-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="208d1-185">Wartość dla **nazwa** automatycznie wypełnić **Nazwa interfejsu API** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="208d1-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="208d1-186">b.</span><span class="sxs-lookup"><span data-stu-id="208d1-186">b.</span></span> <span data-ttu-id="208d1-187">Wklej **identyfikator jednostki SMAL** wartości do **wystawcy** w Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="208d1-188">c.</span><span class="sxs-lookup"><span data-stu-id="208d1-188">c.</span></span> <span data-ttu-id="208d1-189">W **textbox identyfikator jednostki**, wpisz nazwę domeny witryny Salesforce przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="208d1-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="208d1-190">Konto przedsiębiorstwa:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="208d1-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="208d1-191">Konta dewelopera:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="208d1-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="208d1-192">d.</span><span class="sxs-lookup"><span data-stu-id="208d1-192">d.</span></span> <span data-ttu-id="208d1-193">Kliknij przycisk **Przeglądaj** lub **wybierz plik** otworzyć **wybierz plik do przekazania** okno dialogowe, wybierz certyfikat usług Salesforce, a następnie kliknij przycisk **Otwórz** można przekazać certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="208d1-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="208d1-194">e.</span><span class="sxs-lookup"><span data-stu-id="208d1-194">e.</span></span> <span data-ttu-id="208d1-195">Dla **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera użytkownika witryny salesforce.com**.</span><span class="sxs-lookup"><span data-stu-id="208d1-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="208d1-196">f.</span><span class="sxs-lookup"><span data-stu-id="208d1-196">f.</span></span> <span data-ttu-id="208d1-197">Dla **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier instrukcji podmiotu**</span><span class="sxs-lookup"><span data-stu-id="208d1-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="208d1-198">g.</span><span class="sxs-lookup"><span data-stu-id="208d1-198">g.</span></span> <span data-ttu-id="208d1-199">Wklej **pojedynczy znak na adres URL usługi** do **adresu URL logowania do dostawcy tożsamości** w Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="208d1-200">h.</span><span class="sxs-lookup"><span data-stu-id="208d1-200">h.</span></span> <span data-ttu-id="208d1-201">Dla **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **przekierowywanie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="208d1-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="208d1-202">i.</span><span class="sxs-lookup"><span data-stu-id="208d1-202">i.</span></span> <span data-ttu-id="208d1-203">Na koniec kliknij **zapisać** dotyczyć SAML pojedynczego logowania jednokrotnego ustawień.</span><span class="sxs-lookup"><span data-stu-id="208d1-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="208d1-204">W lewym okienku nawigacji w aplikacji Salesforce, kliknij polecenie **Zarządzanie domenami** rozwiń sekcję powiązane, a następnie kliknij przycisk **Moje domeny**.</span><span class="sxs-lookup"><span data-stu-id="208d1-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="208d1-206">Przewiń w dół do **konfiguracji uwierzytelniania** sekcji, a następnie kliknij polecenie **Edytuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="208d1-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="208d1-208">W **usługi uwierzytelniania** sekcji, wybierz przyjazną nazwę konfiguracji logowania jednokrotnego SAML, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="208d1-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="208d1-210">Jeśli zostanie wybrana więcej niż jedna usługa uwierzytelniania, użytkownicy są monit o wybranie usługi uwierzytelniania, która ich, takich jak się zalogować podczas inicjowania rejestracji jednokrotnej w środowisku usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="208d1-211">Jeśli nie chcesz, aby mieć miejsce, a następnie wykonaj następujące czynności **pozostawienie jej niezaznaczonej innych usług uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="208d1-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="208d1-212">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="208d1-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="208d1-213">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="208d1-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="208d1-214">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="208d1-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="208d1-215">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="208d1-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="208d1-216">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="208d1-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="208d1-218">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="208d1-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="208d1-219">W lewym okienku nawigacji w **portalu Azure**, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="208d1-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="208d1-221">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="208d1-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="208d1-223">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="208d1-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="208d1-225">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="208d1-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="208d1-227">a.</span><span class="sxs-lookup"><span data-stu-id="208d1-227">a.</span></span> <span data-ttu-id="208d1-228">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="208d1-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="208d1-229">b.</span><span class="sxs-lookup"><span data-stu-id="208d1-229">b.</span></span> <span data-ttu-id="208d1-230">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="208d1-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="208d1-231">c.</span><span class="sxs-lookup"><span data-stu-id="208d1-231">c.</span></span> <span data-ttu-id="208d1-232">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="208d1-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="208d1-233">d.</span><span class="sxs-lookup"><span data-stu-id="208d1-233">d.</span></span> <span data-ttu-id="208d1-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="208d1-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="208d1-235">Tworzenie użytkownika testowego usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="208d1-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="208d1-236">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="208d1-237">SalesForce obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="208d1-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="208d1-238">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="208d1-238">There is no action item for you in this section.</span></span> <span data-ttu-id="208d1-239">Jeśli użytkownik nie istnieje w usłudze Salesforce, nowy jest tworzony przy próbie uzyskania dostępu do usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="208d1-240">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="208d1-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="208d1-241">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="208d1-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="208d1-243">**Aby przypisać Simona Britta Salesforce, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="208d1-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="208d1-244">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="208d1-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="208d1-246">Na liście aplikacji zaznacz **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="208d1-246">In the applications list, select **Salesforce**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="208d1-248">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="208d1-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="208d1-250">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="208d1-250">Click **Add** button.</span></span> <span data-ttu-id="208d1-251">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="208d1-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="208d1-253">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="208d1-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="208d1-254">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="208d1-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="208d1-255">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="208d1-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="208d1-256">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="208d1-256">Testing single sign-on</span></span>

<span data-ttu-id="208d1-257">Aby przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu w [https://myapps.microsoft.com](https://myapps.microsoft.com/), następnie zaloguj się do konta testowego i kliknij przycisk **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="208d1-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="208d1-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="208d1-258">Additional resources</span></span>

* [<span data-ttu-id="208d1-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="208d1-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="208d1-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="208d1-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="208d1-261">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="208d1-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

