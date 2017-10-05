---
title: 'Samouczek: Integracji Azure Active Directory z DocuSign | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="efa50-103">Samouczek: Integracji Azure Active Directory z DocuSign</span><span class="sxs-lookup"><span data-stu-id="efa50-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="efa50-104">Z tego samouczka dowiesz się integrowanie DocuSign z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="efa50-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efa50-105">Integracja z usługą Azure AD DocuSign zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="efa50-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="efa50-106">Można kontrolować w usłudze Azure AD, który ma dostęp do DocuSign</span><span class="sxs-lookup"><span data-stu-id="efa50-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="efa50-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do DocuSign (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa50-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efa50-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="efa50-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="efa50-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efa50-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efa50-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="efa50-110">Prerequisites</span></span>

<span data-ttu-id="efa50-111">Aby skonfigurować integrację usługi Azure AD z DocuSign, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="efa50-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="efa50-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efa50-113">DocuSign logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="efa50-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="efa50-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="efa50-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="efa50-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="efa50-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efa50-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="efa50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="efa50-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efa50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efa50-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="efa50-118">Scenario description</span></span>
<span data-ttu-id="efa50-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="efa50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="efa50-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="efa50-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efa50-121">Dodawanie DocuSign z galerii</span><span class="sxs-lookup"><span data-stu-id="efa50-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="efa50-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="efa50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="efa50-123">Dodawanie DocuSign z galerii</span><span class="sxs-lookup"><span data-stu-id="efa50-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="efa50-124">Aby skonfigurować integrację usługi Azure AD DocuSign, należy dodać DocuSign z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="efa50-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="efa50-125">**Aby dodać DocuSign z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="efa50-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="efa50-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="efa50-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="efa50-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="efa50-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="efa50-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="efa50-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="efa50-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="efa50-133">W polu wyszukiwania wpisz **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="efa50-133">In the search box, type **DocuSign**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="efa50-135">W panelu wyników wybierz **DocuSign**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="efa50-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efa50-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="efa50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="efa50-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DocuSign na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="efa50-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="efa50-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w DocuSign jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efa50-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="efa50-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w DocuSign musi się.</span><span class="sxs-lookup"><span data-stu-id="efa50-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="efa50-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w DocuSign.</span><span class="sxs-lookup"><span data-stu-id="efa50-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="efa50-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DocuSign, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="efa50-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="efa50-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="efa50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="efa50-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="efa50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="efa50-145">**[Tworzenie użytkownika testowego DocuSign](#creating-a-docusign-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta DocuSign połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="efa50-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="efa50-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="efa50-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efa50-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="efa50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efa50-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="efa50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efa50-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji DocuSign.</span><span class="sxs-lookup"><span data-stu-id="efa50-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="efa50-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z DocuSign, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="efa50-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="efa50-151">W portalu Azure na **DocuSign** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="efa50-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="efa50-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="efa50-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="efa50-155">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base 64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="efa50-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="efa50-157">Na **konfiguracji DocuSign** części portalu Azure, kliknij przycisk **skonfigurować DocuSign** można otworzyć Konfigurowanie logowania jednokrotnego okna.</span><span class="sxs-lookup"><span data-stu-id="efa50-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="efa50-158">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="efa50-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="efa50-160">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **portalu administracyjnego DocuSign** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="efa50-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="efa50-161">W menu nawigacji po lewej stronie kliknij **domen**.</span><span class="sxs-lookup"><span data-stu-id="efa50-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][51]

7. <span data-ttu-id="efa50-163">W okienku po prawej stronie, kliknij polecenie **oświadczenia domeny**.</span><span class="sxs-lookup"><span data-stu-id="efa50-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][52]

8. <span data-ttu-id="efa50-165">Na **oświadczenia domeny** okna dialogowego, w **nazwy domeny** pole tekstowe, wpisz domenę firmy, a następnie kliknij przycisk **oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="efa50-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="efa50-166">Upewnij się, że weryfikowanie domeny i stan jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="efa50-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][53]

9. <span data-ttu-id="efa50-168">W menu po lewej stronie kliknij **dostawców tożsamości**</span><span class="sxs-lookup"><span data-stu-id="efa50-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Konfigurowanie rejestracji jednokrotnej][54]
10. <span data-ttu-id="efa50-170">W okienku po prawej stronie kliknij **Dodawanie dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="efa50-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][55]

11. <span data-ttu-id="efa50-172">Na **ustawień dostawcy tożsamości** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efa50-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][56]

    <span data-ttu-id="efa50-174">a.</span><span class="sxs-lookup"><span data-stu-id="efa50-174">a.</span></span> <span data-ttu-id="efa50-175">W **nazwa** tekstowym, wpisz unikatową nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="efa50-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="efa50-176">Nie należy używać spacji.</span><span class="sxs-lookup"><span data-stu-id="efa50-176">Do not use spaces.</span></span>

    <span data-ttu-id="efa50-177">b.</span><span class="sxs-lookup"><span data-stu-id="efa50-177">b.</span></span> <span data-ttu-id="efa50-178">Wklej **identyfikator jednostki SAML** do **wystawcy dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="efa50-179">c.</span><span class="sxs-lookup"><span data-stu-id="efa50-179">c.</span></span> <span data-ttu-id="efa50-180">Wklej **SAML pojedynczy znak na adres URL usługi** do **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="efa50-181">d.</span><span class="sxs-lookup"><span data-stu-id="efa50-181">d.</span></span> <span data-ttu-id="efa50-182">Wklej **Sign-Out URL** do **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="efa50-183">e.</span><span class="sxs-lookup"><span data-stu-id="efa50-183">e.</span></span> <span data-ttu-id="efa50-184">Wybierz **podpisywania żądania uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="efa50-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="efa50-185">f.</span><span class="sxs-lookup"><span data-stu-id="efa50-185">f.</span></span> <span data-ttu-id="efa50-186">Jako **AuthN wysyłanie żądania przez**, wybierz pozycję **POST**.</span><span class="sxs-lookup"><span data-stu-id="efa50-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="efa50-187">g.</span><span class="sxs-lookup"><span data-stu-id="efa50-187">g.</span></span> <span data-ttu-id="efa50-188">Jako **Wyślij żądanie wylogowania**, wybierz pozycję **UZYSKAĆ**.</span><span class="sxs-lookup"><span data-stu-id="efa50-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="efa50-189">W **mapowanie atrybutu niestandardowego** sekcji, wybierz pole do mapowania oświadczenie, Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efa50-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="efa50-190">W tym przykładzie **emailaddress** oświadczenia jest zamapowana z wartością **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="efa50-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="efa50-191">Jest domyślną nazwę oświadczenia z usługą Azure AD, oświadczenie adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="efa50-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="efa50-192">Użyj odpowiedniej **identyfikator użytkownika** do mapowania użytkownika z usługi Azure AD do mapowania użytkowników DocuSign.</span><span class="sxs-lookup"><span data-stu-id="efa50-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="efa50-193">Zaznacz odpowiednie pola, a następnie wprowadź odpowiednią wartość, na podstawie własnych ustawień organizacji.</span><span class="sxs-lookup"><span data-stu-id="efa50-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Konfigurowanie rejestracji jednokrotnej][57]

13. <span data-ttu-id="efa50-195">W **certyfikat dostawcy tożsamości** , kliknij przycisk **Dodaj certyfikat**, a następnie przekaż certyfikat został pobrany z portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efa50-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Konfigurowanie rejestracji jednokrotnej][58]

14. <span data-ttu-id="efa50-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="efa50-197">Click **Save**.</span></span>

15. <span data-ttu-id="efa50-198">W **dostawców tożsamości** kliknij **akcje**, a następnie kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="efa50-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Konfigurowanie rejestracji jednokrotnej][59]
 
16. <span data-ttu-id="efa50-200">W **Wyświetl SAML 2.0 punkty końcowe** sekcji na **portalu administracyjnego DocuSign**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efa50-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][60]
   
    <span data-ttu-id="efa50-202">a.</span><span class="sxs-lookup"><span data-stu-id="efa50-202">a.</span></span> <span data-ttu-id="efa50-203">Kopiuj **adres URL wystawcy dostawcy usługi**i wkleić do **identyfikator** textbox w **DocuSign domeny i adres URL** części portalu Azure, zgodnie ze wzorcem: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="efa50-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="efa50-204">b.</span><span class="sxs-lookup"><span data-stu-id="efa50-204">b.</span></span> <span data-ttu-id="efa50-205">Kopiuj **adres URL logowania dostawcy usługi**i wkleić do **na adres URL logowania** textbox w **DocuSign domeny i adres URL** części portalu Azure, zgodnie ze wzorcem: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/` .</span><span class="sxs-lookup"><span data-stu-id="efa50-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="efa50-207">c.</span><span class="sxs-lookup"><span data-stu-id="efa50-207">c.</span></span>  <span data-ttu-id="efa50-208">Kliknij przycisk **Zamknij**</span><span class="sxs-lookup"><span data-stu-id="efa50-208">Click **Close**</span></span>
    
17. <span data-ttu-id="efa50-209">W portalu Azure, kliknij polecenie **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="efa50-209">On the Azure portal, click **Save**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="efa50-211">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="efa50-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="efa50-212">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="efa50-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="efa50-213">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="efa50-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efa50-214">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa50-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="efa50-215">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="efa50-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="efa50-217">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="efa50-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="efa50-218">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="efa50-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efa50-220">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="efa50-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efa50-222">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efa50-224">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efa50-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="efa50-226">a.</span><span class="sxs-lookup"><span data-stu-id="efa50-226">a.</span></span> <span data-ttu-id="efa50-227">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efa50-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efa50-228">b.</span><span class="sxs-lookup"><span data-stu-id="efa50-228">b.</span></span> <span data-ttu-id="efa50-229">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="efa50-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="efa50-230">c.</span><span class="sxs-lookup"><span data-stu-id="efa50-230">c.</span></span> <span data-ttu-id="efa50-231">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="efa50-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="efa50-232">d.</span><span class="sxs-lookup"><span data-stu-id="efa50-232">d.</span></span> <span data-ttu-id="efa50-233">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="efa50-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="efa50-234">Tworzenie użytkownika testowego DocuSign</span><span class="sxs-lookup"><span data-stu-id="efa50-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="efa50-235">Aplikacja obsługuje **tylko w czasie Inicjowanie obsługi użytkowników** i po uwierzytelniania użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="efa50-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="efa50-236">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa50-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="efa50-237">W tej sekcji można włączyć Simona Britta do udostępnienia jej DocuSign za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="efa50-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="efa50-239">**Aby przypisać Simona Britta DocuSign, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="efa50-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="efa50-240">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="efa50-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="efa50-242">Na liście aplikacji zaznacz **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="efa50-242">In the applications list, select **DocuSign**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="efa50-244">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="efa50-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="efa50-246">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="efa50-246">Click **Add** button.</span></span> <span data-ttu-id="efa50-247">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="efa50-249">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="efa50-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="efa50-250">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="efa50-251">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="efa50-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="efa50-252">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="efa50-252">Testing single sign-on</span></span>

<span data-ttu-id="efa50-253">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="efa50-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="efa50-254">Po kliknięciu kafelka DocuSign w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji DocuSign.</span><span class="sxs-lookup"><span data-stu-id="efa50-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="efa50-255">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="efa50-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="efa50-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="efa50-256">Additional resources</span></span>

* [<span data-ttu-id="efa50-257">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efa50-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efa50-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="efa50-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="efa50-259">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="efa50-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

