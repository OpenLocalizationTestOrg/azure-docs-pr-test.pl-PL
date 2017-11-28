---
title: 'Samouczek: Integracji Azure Active Directory z Brightspace przez Desire2Learn | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Brightspace przez Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7076b476ba71c5d94ae4728e5f6032b0d7e047ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="a110e-103">Samouczek: Integracji Azure Active Directory z Brightspace przez Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="a110e-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="a110e-104">Z tego samouczka dowiesz się integrowanie Brightspace przez Desire2Learn z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a110e-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a110e-105">Integracja z usługą Azure AD Brightspace przez Desire2Learn zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a110e-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a110e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Brightspace przez Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="a110e-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span></span>
- <span data-ttu-id="a110e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Brightspace przez Desire2Learn (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a110e-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a110e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a110e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a110e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a110e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a110e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a110e-110">Prerequisites</span></span>

<span data-ttu-id="a110e-111">Aby skonfigurować integrację usługi Azure AD z Brightspace przez Desire2Learn, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a110e-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span></span>

- <span data-ttu-id="a110e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a110e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a110e-113">Brightspace przez Desire2Learn logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a110e-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a110e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a110e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a110e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a110e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a110e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a110e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a110e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a110e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a110e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a110e-118">Scenario description</span></span>
<span data-ttu-id="a110e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a110e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a110e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a110e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a110e-121">Dodawanie Brightspace przez Desire2Learn z galerii</span><span class="sxs-lookup"><span data-stu-id="a110e-121">Adding Brightspace by Desire2Learn from the gallery</span></span>
2. <span data-ttu-id="a110e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a110e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-the-gallery"></a><span data-ttu-id="a110e-123">Dodawanie Brightspace przez Desire2Learn z galerii</span><span class="sxs-lookup"><span data-stu-id="a110e-123">Adding Brightspace by Desire2Learn from the gallery</span></span>
<span data-ttu-id="a110e-124">Aby skonfigurować integrację usługi Azure AD Brightspace przez Desire2Learn, należy dodać Brightspace przez Desire2Learn z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a110e-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a110e-125">**Aby dodać Brightspace przez Desire2Learn z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a110e-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a110e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a110e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a110e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a110e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a110e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a110e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a110e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a110e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a110e-133">W polu wyszukiwania wpisz **Brightspace przez Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="a110e-133">In the search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="a110e-135">W panelu wyników wybierz **Brightspace przez Desire2Learn**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a110e-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a110e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a110e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a110e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Brightspace przez Desire2Learn w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a110e-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a110e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Brightspace przez Desire2Learn jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a110e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span></span> <span data-ttu-id="a110e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Brightspace przez Desire2Learn musi się.</span><span class="sxs-lookup"><span data-stu-id="a110e-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span></span>

<span data-ttu-id="a110e-141">W Brightspace przez Desire2Learn, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="a110e-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a110e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Brightspace przez Desire2Learn, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a110e-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a110e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a110e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a110e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a110e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a110e-145">**[Tworzenie Brightspace przez użytkownika testowego Desire2Learn](#creating-a-brightspace-by-desire2learn-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Brightspace przez Desire2Learn połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a110e-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a110e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a110e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a110e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a110e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a110e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a110e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a110e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i konfigurowanie rejestracji jednokrotnej w sieci Brightspace przez aplikację Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="a110e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="a110e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Brightspace przez Desire2Learn, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a110e-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="a110e-151">W portalu Azure na **Brightspace przez Desire2Learn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a110e-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a110e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a110e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="a110e-155">Na **Brightspace Desire2Learn domeny i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a110e-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="a110e-157">a.</span><span class="sxs-lookup"><span data-stu-id="a110e-157">a.</span></span> <span data-ttu-id="a110e-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="a110e-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="a110e-159">b.</span><span class="sxs-lookup"><span data-stu-id="a110e-159">b.</span></span> <span data-ttu-id="a110e-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="a110e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a110e-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a110e-161">These values are not real.</span></span> <span data-ttu-id="a110e-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="a110e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a110e-163">Skontaktuj się z [Brightspace przez zespół pomocy technicznej Desire2Learn](https://www.d2l.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a110e-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span></span>
 


4. <span data-ttu-id="a110e-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a110e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="a110e-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a110e-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a110e-168">Aby skonfigurować logowanie jednokrotne w **Brightspace przez Desire2Learn** stronie, musisz wysłać pobrany **XML metadanych** do [Brightspace przez zespół pomocy technicznej Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="a110e-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="a110e-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="a110e-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a110e-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="a110e-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a110e-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a110e-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a110e-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a110e-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="a110e-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a110e-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a110e-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a110e-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a110e-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a110e-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a110e-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a110e-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a110e-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a110e-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a110e-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a110e-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a110e-184">a.</span><span class="sxs-lookup"><span data-stu-id="a110e-184">a.</span></span> <span data-ttu-id="a110e-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a110e-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a110e-186">b.</span><span class="sxs-lookup"><span data-stu-id="a110e-186">b.</span></span> <span data-ttu-id="a110e-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a110e-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a110e-188">c.</span><span class="sxs-lookup"><span data-stu-id="a110e-188">c.</span></span> <span data-ttu-id="a110e-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a110e-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a110e-190">d.</span><span class="sxs-lookup"><span data-stu-id="a110e-190">d.</span></span> <span data-ttu-id="a110e-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a110e-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="a110e-192">Tworzenie Brightspace przez Desire2Learn użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="a110e-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="a110e-193">Aby włączyć użytkowników usługi Azure AD zalogować się do Brightspace przez Desire2Learn, ich muszą mieć przydzielone do Brightspace przez Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="a110e-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="a110e-194">W przypadku Brightspace przez Desire2Learn, konta użytkowników muszą zostać utworzone przez użytkownika [Brightspace przez zespół pomocy technicznej Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="a110e-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="a110e-195">Aby użyć innych Brightspace Desire2Learn narzędzia do tworzenia konta użytkownika lub interfejsów API dostarczonych przez Brightspace przez Desire2Learn do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a110e-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a110e-196">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a110e-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a110e-197">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Brightspace przez Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="a110e-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a110e-199">**Aby przypisać Simona Britta Brightspace przez Desire2Learn, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a110e-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="a110e-200">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a110e-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a110e-202">Na liście aplikacji zaznacz **Brightspace przez Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="a110e-202">In the applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="a110e-204">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a110e-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a110e-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a110e-206">Click **Add** button.</span></span> <span data-ttu-id="a110e-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a110e-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a110e-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a110e-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a110e-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a110e-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a110e-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a110e-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a110e-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a110e-212">Testing single sign-on</span></span>

<span data-ttu-id="a110e-213">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a110e-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a110e-214">Kliknięcie Brightspace Desire2Learn kafelka w panelu dostępu, możesz należy pobrać automatycznie zalogowane do Twojej Brightspace przez aplikację Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="a110e-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="a110e-215">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a110e-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a110e-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a110e-216">Additional resources</span></span>

* [<span data-ttu-id="a110e-217">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a110e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a110e-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a110e-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

