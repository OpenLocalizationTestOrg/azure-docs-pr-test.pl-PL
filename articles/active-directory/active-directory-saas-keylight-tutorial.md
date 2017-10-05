---
title: 'Samouczek: Integracji Azure Active Directory z LockPath Keylight | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="7ebdf-103">Samouczek: Integracji Azure Active Directory z LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="7ebdf-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="7ebdf-104">Z tego samouczka dowiesz się integrowanie LockPath Keylight z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ebdf-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ebdf-105">Integracja z usługą Azure AD LockPath Keylight zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ebdf-106">Można kontrolować w usłudze Azure AD, który ma dostęp do LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="7ebdf-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="7ebdf-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do LockPath Keylight (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebdf-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ebdf-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7ebdf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ebdf-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ebdf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ebdf-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7ebdf-110">Prerequisites</span></span>

<span data-ttu-id="7ebdf-111">Aby skonfigurować integrację usługi Azure AD z LockPath Keylight, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="7ebdf-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebdf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ebdf-113">LockPath Keylight jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7ebdf-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ebdf-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ebdf-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ebdf-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ebdf-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ebdf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ebdf-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7ebdf-118">Scenario description</span></span>
<span data-ttu-id="7ebdf-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ebdf-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ebdf-121">Dodawanie LockPath Keylight z galerii</span><span class="sxs-lookup"><span data-stu-id="7ebdf-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="7ebdf-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7ebdf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="7ebdf-123">Dodawanie LockPath Keylight z galerii</span><span class="sxs-lookup"><span data-stu-id="7ebdf-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="7ebdf-124">Aby skonfigurować integrację usługi Azure AD LockPath Keylight, należy dodać LockPath Keylight z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ebdf-125">**Aby dodać LockPath Keylight z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7ebdf-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebdf-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7ebdf-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ebdf-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7ebdf-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7ebdf-133">W polu wyszukiwania wpisz **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="7ebdf-135">W panelu wyników wybierz **LockPath Keylight**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ebdf-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7ebdf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ebdf-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z LockPath Keylight oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7ebdf-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7ebdf-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w LockPath Keylight jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="7ebdf-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w LockPath Keylight musi się.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="7ebdf-141">W LockPath Keylight, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ebdf-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LockPath Keylight, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ebdf-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ebdf-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ebdf-145">**[Tworzenie użytkownika testowego LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LockPath Keylight, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ebdf-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ebdf-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ebdf-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7ebdf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ebdf-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="7ebdf-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LockPath Keylight, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7ebdf-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebdf-151">W portalu Azure na **LockPath Keylight** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7ebdf-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="7ebdf-155">Na **LockPath Keylight domeny i adres URL** sekcji, wykonaj następujące kroki::</span><span class="sxs-lookup"><span data-stu-id="7ebdf-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="7ebdf-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-157">a.</span></span> <span data-ttu-id="7ebdf-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="7ebdf-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="7ebdf-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-159">b.</span></span> <span data-ttu-id="7ebdf-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="7ebdf-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="7ebdf-161">c.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-161">c.</span></span> <span data-ttu-id="7ebdf-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="7ebdf-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="7ebdf-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-163">These values are not real.</span></span> <span data-ttu-id="7ebdf-164">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7ebdf-165">Skontaktuj się z [zespołem pomocy technicznej klienta Keylight LockPath](https://www.lockpath.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="7ebdf-166">Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="7ebdf-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="7ebdf-170">Na **LockPath Keylight konfiguracji** kliknij **skonfigurować LockPath Keylight** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ebdf-171">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7ebdf-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="7ebdf-173">Aby włączyć logowanie Jednokrotne w LockPath Keylight, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="7ebdf-174">a.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-174">a.</span></span> <span data-ttu-id="7ebdf-175">Logowanie do konta LockPath Keylight jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="7ebdf-176">b.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-176">b.</span></span> <span data-ttu-id="7ebdf-177">W menu u góry kliknij **osoby**i wybierz **Keylight Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="7ebdf-179">c.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-179">c.</span></span> <span data-ttu-id="7ebdf-180">W widoku drzewa po lewej stronie, kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="7ebdf-182">d.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-182">d.</span></span> <span data-ttu-id="7ebdf-183">Na **ustawienia SAML** okna dialogowego, kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="7ebdf-185">Na **edytowanie ustawień SAML** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="7ebdf-187">a.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-187">a.</span></span> <span data-ttu-id="7ebdf-188">Ustaw **uwierzytelnianie SAML** do **Active**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="7ebdf-189">b.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-189">b.</span></span> <span data-ttu-id="7ebdf-190">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="7ebdf-191">c.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-191">c.</span></span> <span data-ttu-id="7ebdf-192">Wklej **pojedynczy adres URL usługi Sign-Out** wartość, która została skopiowana z portalu Azure do **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="7ebdf-193">d.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-193">d.</span></span> <span data-ttu-id="7ebdf-194">Kliknij przycisk **wybierz plik** wybierz pobranego certyfikatu LockPath Keylight, a następnie kliknij przycisk **Otwórz** można przekazać certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="7ebdf-195">e.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-195">e.</span></span> <span data-ttu-id="7ebdf-196">Ustaw **lokalizacji identyfikator użytkownika SAML** do **elementu NameIdentifier instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="7ebdf-197">f.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-197">f.</span></span> <span data-ttu-id="7ebdf-198">Podaj **dostawcy usług Keylight** przy użyciu następującego wzorca: **https://&lt;NazwaFirmy&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="7ebdf-199">g.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-199">g.</span></span> <span data-ttu-id="7ebdf-200">Ustaw **automatycznego udostępniania użytkownikom** do **Active**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="7ebdf-201">h.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-201">h.</span></span> <span data-ttu-id="7ebdf-202">Ustaw **typ konta Auto-provision** do **pełnej**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="7ebdf-203">i.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-203">i.</span></span> <span data-ttu-id="7ebdf-204">Ustaw **roli zabezpieczeń Auto-provision**, wybierz pozycję **użytkowników standardowych z SAML**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="7ebdf-205">j.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-205">j.</span></span> <span data-ttu-id="7ebdf-206">Ustaw **konfiguracji zabezpieczeń Auto-provision**, wybierz pozycję **standardowej konfiguracji użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="7ebdf-207">k.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-207">k.</span></span> <span data-ttu-id="7ebdf-208">W **atrybut poczty E-mail** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="7ebdf-209">l.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-209">l.</span></span> <span data-ttu-id="7ebdf-210">W **atrybutu imię** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="7ebdf-211">m.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-211">m.</span></span> <span data-ttu-id="7ebdf-212">W **ostatniego atrybutu name** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="7ebdf-213">n.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-213">n.</span></span> <span data-ttu-id="7ebdf-214">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7ebdf-215">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="7ebdf-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ebdf-216">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ebdf-217">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ebdf-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ebdf-218">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebdf-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ebdf-219">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7ebdf-221">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7ebdf-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebdf-222">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ebdf-224">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ebdf-226">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ebdf-228">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7ebdf-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ebdf-230">a.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-230">a.</span></span> <span data-ttu-id="7ebdf-231">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ebdf-232">b.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-232">b.</span></span> <span data-ttu-id="7ebdf-233">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ebdf-234">c.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-234">c.</span></span> <span data-ttu-id="7ebdf-235">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ebdf-236">d.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-236">d.</span></span> <span data-ttu-id="7ebdf-237">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="7ebdf-238">Tworzenie użytkownika testowego LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="7ebdf-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="7ebdf-239">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="7ebdf-240">LockPath Keylight obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="7ebdf-241">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-241">There is no action item for you in this section.</span></span> <span data-ttu-id="7ebdf-242">Nowy użytkownik jest tworzony podczas uzyskiwania dostępu do LockPath Keylight, jeśli użytkownik nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="7ebdf-243">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej klienta Keylight LockPath](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="7ebdf-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ebdf-244">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebdf-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ebdf-245">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7ebdf-247">**Aby przypisać Simona Britta LockPath Keylight, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7ebdf-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebdf-248">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7ebdf-250">Na liście aplikacji zaznacz **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="7ebdf-252">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7ebdf-254">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-254">Click **Add** button.</span></span> <span data-ttu-id="7ebdf-255">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7ebdf-257">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ebdf-258">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ebdf-259">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ebdf-260">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7ebdf-260">Testing single sign-on</span></span>

<span data-ttu-id="7ebdf-261">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7ebdf-262">Po kliknięciu kafelka LockPath Keylight w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="7ebdf-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7ebdf-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7ebdf-263">Additional resources</span></span>

* [<span data-ttu-id="7ebdf-264">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ebdf-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ebdf-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ebdf-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

