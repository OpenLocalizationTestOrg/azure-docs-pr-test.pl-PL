---
title: 'Samouczek: Integracji Azure Active Directory z UserVoice | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="826bd-103">Samouczek: Integracji Azure Active Directory z UserVoice</span><span class="sxs-lookup"><span data-stu-id="826bd-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="826bd-104">Z tego samouczka dowiesz się Integrowanie usługi UserVoice w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="826bd-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="826bd-105">Integrowanie UserVoice w usłudze Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="826bd-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="826bd-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługi UserVoice.</span><span class="sxs-lookup"><span data-stu-id="826bd-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="826bd-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do środowiska UserVoice (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="826bd-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="826bd-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="826bd-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="826bd-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="826bd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="826bd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="826bd-110">Prerequisites</span></span>

<span data-ttu-id="826bd-111">Aby skonfigurować integrację usługi Azure AD z UserVoice, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="826bd-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="826bd-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="826bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="826bd-113">UserVoice logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="826bd-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="826bd-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="826bd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="826bd-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="826bd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="826bd-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="826bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="826bd-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="826bd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="826bd-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="826bd-118">Scenario description</span></span>
<span data-ttu-id="826bd-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="826bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="826bd-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="826bd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="826bd-121">Dodawanie UserVoice z galerii</span><span class="sxs-lookup"><span data-stu-id="826bd-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="826bd-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="826bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="826bd-123">Dodawanie UserVoice z galerii</span><span class="sxs-lookup"><span data-stu-id="826bd-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="826bd-124">Aby skonfigurować integrację usługi UserVoice w usłudze Azure Active Directory, należy dodać UserVoice z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="826bd-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="826bd-125">**Aby dodać UserVoice z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="826bd-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="826bd-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="826bd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="826bd-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="826bd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="826bd-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="826bd-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="826bd-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="826bd-133">W polu wyszukiwania wpisz **UserVoice**, wybierz pozycję **UserVoice** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="826bd-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![UserVoice na liście wyników](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="826bd-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="826bd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="826bd-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UserVoice w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="826bd-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w UserVoice jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="826bd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="826bd-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w UserVoice musi się.</span><span class="sxs-lookup"><span data-stu-id="826bd-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="826bd-139">W UserVoice, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="826bd-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="826bd-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UserVoice, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="826bd-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="826bd-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="826bd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="826bd-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="826bd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="826bd-143">**[Tworzenie użytkownika testowego UserVoice](#create-a-uservoice-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta UserVoice połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="826bd-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="826bd-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="826bd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="826bd-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="826bd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="826bd-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="826bd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="826bd-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji UserVoice.</span><span class="sxs-lookup"><span data-stu-id="826bd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="826bd-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z UserVoice, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="826bd-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="826bd-149">W portalu Azure na **UserVoice** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="826bd-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="826bd-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="826bd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="826bd-153">Na **UserVoice domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="826bd-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny UserVoice pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="826bd-155">a.</span><span class="sxs-lookup"><span data-stu-id="826bd-155">a.</span></span> <span data-ttu-id="826bd-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="826bd-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="826bd-157">b.</span><span class="sxs-lookup"><span data-stu-id="826bd-157">b.</span></span> <span data-ttu-id="826bd-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="826bd-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="826bd-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="826bd-159">These values are not real.</span></span> <span data-ttu-id="826bd-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="826bd-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="826bd-161">Skontaktuj się z [zespołem pomocy technicznej klienta UserVoice](https://www.uservoice.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="826bd-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="826bd-162">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="826bd-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="826bd-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="826bd-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="826bd-166">Na **konfiguracji UserVoice** , kliknij przycisk **skonfigurować UserVoice** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="826bd-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="826bd-167">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="826bd-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja usługi UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="826bd-169">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy UserVoice.</span><span class="sxs-lookup"><span data-stu-id="826bd-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="826bd-170">Na pasku narzędzi u góry kliknij **ustawienia**, a następnie wybierz **portalu sieci Web** z menu.</span><span class="sxs-lookup"><span data-stu-id="826bd-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="826bd-171">![W sekcji Ustawienia na stronie aplikacji](./media/active-directory-saas-uservoice-tutorial/ic777519.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="826bd-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="826bd-172">Na **portalu sieci Web** karcie **uwierzytelnianie użytkownika** , kliknij przycisk **Edytuj** otworzyć **Edytuj uwierzytelnianie użytkownika** strony okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="826bd-173">![Portal sieci Web kartę](./media/active-directory-saas-uservoice-tutorial/ic777520.png "portalu sieci Web")</span><span class="sxs-lookup"><span data-stu-id="826bd-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="826bd-174">Na **Edytuj uwierzytelnianie użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="826bd-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="826bd-175">![Edytuj uwierzytelnianie użytkownika](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edytuj uwierzytelnianie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="826bd-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="826bd-176">a.</span><span class="sxs-lookup"><span data-stu-id="826bd-176">a.</span></span> <span data-ttu-id="826bd-177">Kliknij przycisk **logowanie jednokrotne (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="826bd-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="826bd-178">b.</span><span class="sxs-lookup"><span data-stu-id="826bd-178">b.</span></span> <span data-ttu-id="826bd-179">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **logowania jednokrotnego zdalnego logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="826bd-180">c.</span><span class="sxs-lookup"><span data-stu-id="826bd-180">c.</span></span> <span data-ttu-id="826bd-181">Wklej **Sign-Out URL** wartość, która została skopiowana z portalu Azure do **Sign-Out zdalnego logowania jednokrotnego textbox**.</span><span class="sxs-lookup"><span data-stu-id="826bd-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="826bd-182">d.</span><span class="sxs-lookup"><span data-stu-id="826bd-182">d.</span></span> <span data-ttu-id="826bd-183">Wklej **odcisk palca** wartość, która została skopiowana z portalu Azure do **bieżącego odcisk palca certyfikatu SHA1** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="826bd-184">e.</span><span class="sxs-lookup"><span data-stu-id="826bd-184">e.</span></span> <span data-ttu-id="826bd-185">Kliknij przycisk **Zapisz ustawienia uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="826bd-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="826bd-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="826bd-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="826bd-187">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="826bd-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="826bd-188">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="826bd-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="826bd-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="826bd-189">Create an Azure AD test user</span></span>

<span data-ttu-id="826bd-190">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="826bd-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="826bd-192">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="826bd-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="826bd-193">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="826bd-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="826bd-195">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="826bd-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="826bd-197">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="826bd-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="826bd-199">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="826bd-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="826bd-201">a.</span><span class="sxs-lookup"><span data-stu-id="826bd-201">a.</span></span> <span data-ttu-id="826bd-202">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="826bd-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="826bd-203">b.</span><span class="sxs-lookup"><span data-stu-id="826bd-203">b.</span></span> <span data-ttu-id="826bd-204">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="826bd-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="826bd-205">c.</span><span class="sxs-lookup"><span data-stu-id="826bd-205">c.</span></span> <span data-ttu-id="826bd-206">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="826bd-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="826bd-207">d.</span><span class="sxs-lookup"><span data-stu-id="826bd-207">d.</span></span> <span data-ttu-id="826bd-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="826bd-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="826bd-209">Tworzenie użytkownika testowego UserVoice</span><span class="sxs-lookup"><span data-stu-id="826bd-209">Create a UserVoice test user</span></span>

<span data-ttu-id="826bd-210">Aby umożliwić użytkownikom usługi Azure AD do logowania się w usłudze UserVoice, musi być przygotowana do UserVoice.</span><span class="sxs-lookup"><span data-stu-id="826bd-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="826bd-211">W przypadku UserVoice Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="826bd-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="826bd-212">Aby udostępnić konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="826bd-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="826bd-213">Zaloguj się do Twojego **UserVoice** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="826bd-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="826bd-214">Przejdź do **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="826bd-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="826bd-215">![Ustawienia](./media/active-directory-saas-uservoice-tutorial/ic777811.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="826bd-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="826bd-216">Kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="826bd-216">Click **General**.</span></span>

4. <span data-ttu-id="826bd-217">Kliknij przycisk **agentów i uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="826bd-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="826bd-218">![Agenci i uprawnienia](./media/active-directory-saas-uservoice-tutorial/ic777812.png "agentów i uprawnień")</span><span class="sxs-lookup"><span data-stu-id="826bd-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="826bd-219">Kliknij przycisk **dodać Administratorzy**.</span><span class="sxs-lookup"><span data-stu-id="826bd-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="826bd-220">![Dodaj administratorów](./media/active-directory-saas-uservoice-tutorial/ic777813.png "dodać administratorów")</span><span class="sxs-lookup"><span data-stu-id="826bd-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="826bd-221">Na **zaprosić Administratorzy** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="826bd-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="826bd-222">![Zaproś Administratorzy](./media/active-directory-saas-uservoice-tutorial/ic777814.png "zaprosić Administratorzy")</span><span class="sxs-lookup"><span data-stu-id="826bd-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="826bd-223">a.</span><span class="sxs-lookup"><span data-stu-id="826bd-223">a.</span></span> <span data-ttu-id="826bd-224">W polu tekstowym wiadomości E-mail, wpisz adres e-mail konta, aby udostępnić, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="826bd-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="826bd-225">b.</span><span class="sxs-lookup"><span data-stu-id="826bd-225">b.</span></span> <span data-ttu-id="826bd-226">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="826bd-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="826bd-227">Możesz użyć innych UserVoice użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez UserVoice do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="826bd-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="826bd-228">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="826bd-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="826bd-229">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do środowiska UserVoice.</span><span class="sxs-lookup"><span data-stu-id="826bd-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="826bd-231">**Aby przypisać Simona Britta UserVoice, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="826bd-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="826bd-232">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="826bd-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="826bd-234">Na liście aplikacji zaznacz **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="826bd-234">In the applications list, select **UserVoice**.</span></span>

    ![Łącze UserVoice na liście aplikacji](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="826bd-236">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="826bd-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="826bd-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="826bd-238">Click **Add** button.</span></span> <span data-ttu-id="826bd-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="826bd-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="826bd-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="826bd-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="826bd-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="826bd-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="826bd-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="826bd-244">Test single sign-on</span></span>

<span data-ttu-id="826bd-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="826bd-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="826bd-246">Po kliknięciu kafelka UserVoice w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi UserVoice.</span><span class="sxs-lookup"><span data-stu-id="826bd-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="826bd-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="826bd-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="826bd-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="826bd-248">Additional resources</span></span>

* [<span data-ttu-id="826bd-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="826bd-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="826bd-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="826bd-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

