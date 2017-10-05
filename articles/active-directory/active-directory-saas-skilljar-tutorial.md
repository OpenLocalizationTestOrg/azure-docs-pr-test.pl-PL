---
title: 'Samouczek: Integracji Azure Active Directory z Skilljar | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Skilljar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c572f556-98a3-48e6-8e4c-e634b7a2ba70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d5238a0471b6ae4b367ca5c1ed5e1f273a0c476b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skilljar"></a><span data-ttu-id="8a373-103">Samouczek: Integracji Azure Active Directory z Skilljar</span><span class="sxs-lookup"><span data-stu-id="8a373-103">Tutorial: Azure Active Directory integration with Skilljar</span></span>

<span data-ttu-id="8a373-104">Z tego samouczka dowiesz się integrowanie Skilljar z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a373-104">In this tutorial, you learn how to integrate Skilljar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a373-105">Integracja z usługą Azure AD Skilljar zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8a373-105">Integrating Skilljar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a373-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Skilljar</span><span class="sxs-lookup"><span data-stu-id="8a373-106">You can control in Azure AD who has access to Skilljar</span></span>
- <span data-ttu-id="8a373-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Skilljar (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a373-107">You can enable your users to automatically get signed-on to Skilljar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a373-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8a373-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a373-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a373-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a373-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8a373-110">Prerequisites</span></span>

<span data-ttu-id="8a373-111">Aby skonfigurować integrację usługi Azure AD z Skilljar, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8a373-111">To configure Azure AD integration with Skilljar, you need the following items:</span></span>

- <span data-ttu-id="8a373-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a373-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a373-113">Skilljar logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8a373-113">A Skilljar single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a373-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8a373-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a373-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8a373-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a373-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8a373-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a373-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a373-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a373-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8a373-118">Scenario description</span></span>
<span data-ttu-id="8a373-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8a373-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a373-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8a373-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a373-121">Dodawanie Skilljar z galerii</span><span class="sxs-lookup"><span data-stu-id="8a373-121">Adding Skilljar from the gallery</span></span>
2. <span data-ttu-id="8a373-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8a373-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skilljar-from-the-gallery"></a><span data-ttu-id="8a373-123">Dodawanie Skilljar z galerii</span><span class="sxs-lookup"><span data-stu-id="8a373-123">Adding Skilljar from the gallery</span></span>
<span data-ttu-id="8a373-124">Aby skonfigurować integrację usługi Azure AD Skilljar, należy dodać Skilljar z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8a373-124">To configure the integration of Skilljar into Azure AD, you need to add Skilljar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a373-125">**Aby dodać Skilljar z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8a373-125">**To add Skilljar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a373-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8a373-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8a373-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8a373-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a373-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8a373-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8a373-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a373-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8a373-133">W polu wyszukiwania wpisz **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="8a373-133">In the search box, type **Skilljar**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_search.png)

5. <span data-ttu-id="8a373-135">W panelu wyników wybierz **Skilljar**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8a373-135">In the results panel, select **Skilljar**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a373-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8a373-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a373-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Skilljar w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8a373-138">In this section, you configure and test Azure AD single sign-on with Skilljar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a373-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Skilljar jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a373-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skilljar is to a user in Azure AD.</span></span> <span data-ttu-id="8a373-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Skilljar musi się.</span><span class="sxs-lookup"><span data-stu-id="8a373-140">In other words, a link relationship between an Azure AD user and the related user in Skilljar needs to be established.</span></span>

<span data-ttu-id="8a373-141">W Skilljar, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8a373-141">In Skilljar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a373-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Skilljar, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8a373-142">To configure and test Azure AD single sign-on with Skilljar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a373-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8a373-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a373-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8a373-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a373-145">**[Tworzenie użytkownika testowego Skilljar](#creating-a-skilljar-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Skilljar połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8a373-145">**[Creating a Skilljar test user](#creating-a-skilljar-test-user)** - to have a counterpart of Britta Simon in Skilljar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a373-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8a373-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a373-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8a373-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a373-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8a373-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a373-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8a373-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skilljar application.</span></span>

<span data-ttu-id="8a373-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Skilljar, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8a373-150">**To configure Azure AD single sign-on with Skilljar, perform the following steps:**</span></span>

1. <span data-ttu-id="8a373-151">W portalu Azure na **Skilljar** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8a373-151">In the Azure portal, on the **Skilljar** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8a373-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8a373-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_samlbase.png)

3. <span data-ttu-id="8a373-155">Na **Skilljar domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8a373-155">On the **Skilljar Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_url.png)

    <span data-ttu-id="8a373-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a373-157">a.</span></span> <span data-ttu-id="8a373-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="8a373-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span></span>

    <span data-ttu-id="8a373-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a373-159">b.</span></span> <span data-ttu-id="8a373-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="8a373-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a373-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8a373-161">These values are not real.</span></span> <span data-ttu-id="8a373-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8a373-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a373-163">Skontaktuj się z [zespołem pomocy technicznej klienta Skilljar](http://support.skilljar.com/hc/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="8a373-163">Contact [Skilljar Client support team](http://support.skilljar.com/hc/) to get these values.</span></span> 
 
4. <span data-ttu-id="8a373-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8a373-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_certificate.png) 

5. <span data-ttu-id="8a373-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a373-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skilljar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a373-168">Skonfigurować logowanie jednokrotne w **Skilljar** stronie, musisz wysłać pobrany **XML metadanych**, i **wartość Format identyfikatora nazwy - urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress** do [zespołem pomocy technicznej Skilljar](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="8a373-168">To configure single sign-on on **Skilljar** side, you need to send the downloaded **Metadata XML**, and **Name Identifier Format Value - urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** to [Skilljar support team](http://support.skilljar.com/hc/).</span></span> <span data-ttu-id="8a373-169">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="8a373-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8a373-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8a373-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a373-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8a373-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a373-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a373-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a373-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a373-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a373-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8a373-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8a373-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8a373-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a373-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8a373-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a373-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8a373-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a373-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a373-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a373-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8a373-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a373-185">a.</span><span class="sxs-lookup"><span data-stu-id="8a373-185">a.</span></span> <span data-ttu-id="8a373-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a373-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a373-187">b.</span><span class="sxs-lookup"><span data-stu-id="8a373-187">b.</span></span> <span data-ttu-id="8a373-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a373-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a373-189">c.</span><span class="sxs-lookup"><span data-stu-id="8a373-189">c.</span></span> <span data-ttu-id="8a373-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8a373-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a373-191">d.</span><span class="sxs-lookup"><span data-stu-id="8a373-191">d.</span></span> <span data-ttu-id="8a373-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8a373-192">Click **Create**.</span></span>
 
### <a name="creating-a-skilljar-test-user"></a><span data-ttu-id="8a373-193">Tworzenie użytkownika testowego Skilljar</span><span class="sxs-lookup"><span data-stu-id="8a373-193">Creating a Skilljar test user</span></span>

<span data-ttu-id="8a373-194">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8a373-194">The objective of this section is to create a user called Britta Simon in Skilljar.</span></span> <span data-ttu-id="8a373-195">Skilljar obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="8a373-195">Skilljar supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8a373-196">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8a373-196">There is no action item for you in this section.</span></span> <span data-ttu-id="8a373-197">Nowy użytkownik został utworzony podczas próby dostępu Skilljar, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8a373-197">A new user is created during an attempt to access Skilljar if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="8a373-198">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Skilljar](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="8a373-198">If you need to create a user manually, you need to contact the [Skilljar support team](http://support.skilljar.com/hc/).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a373-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a373-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a373-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8a373-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skilljar.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8a373-202">**Aby przypisać Simona Britta Skilljar, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8a373-202">**To assign Britta Simon to Skilljar, perform the following steps:**</span></span>

1. <span data-ttu-id="8a373-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8a373-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8a373-205">Na liście aplikacji zaznacz **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="8a373-205">In the applications list, select **Skilljar**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_app.png) 

3. <span data-ttu-id="8a373-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8a373-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8a373-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a373-209">Click **Add** button.</span></span> <span data-ttu-id="8a373-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a373-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8a373-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8a373-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a373-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a373-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a373-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a373-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a373-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8a373-215">Testing single sign-on</span></span>

<span data-ttu-id="8a373-216">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8a373-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="8a373-217">Po kliknięciu kafelka Skilljar w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8a373-217">When you click the Skilljar tile in the Access Panel, you should get automatically signed-on to your Skilljar application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a373-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8a373-218">Additional resources</span></span>

* [<span data-ttu-id="8a373-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a373-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a373-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a373-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_203.png

