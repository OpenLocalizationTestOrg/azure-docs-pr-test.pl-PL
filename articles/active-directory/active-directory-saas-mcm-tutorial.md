---
title: 'Samouczek: Integracji Azure Active Directory z MCM | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i MCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: cbbb0f54b7954c0ec7326fb62bb427155527cc84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="bc031-103">Samouczek: Integracji Azure Active Directory z MCM</span><span class="sxs-lookup"><span data-stu-id="bc031-103">Tutorial: Azure Active Directory integration with MCM</span></span>

<span data-ttu-id="bc031-104">Z tego samouczka dowiesz się integrowanie MCM w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc031-104">In this tutorial, you learn how to integrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bc031-105">Integracja z usługą Azure AD MCM zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bc031-105">Integrating MCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bc031-106">Można kontrolować w usłudze Azure AD, który ma dostęp do MCM</span><span class="sxs-lookup"><span data-stu-id="bc031-106">You can control in Azure AD who has access to MCM</span></span>
- <span data-ttu-id="bc031-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do MCM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc031-107">You can enable your users to automatically get signed-on to MCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bc031-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bc031-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bc031-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bc031-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc031-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc031-110">Prerequisites</span></span>

<span data-ttu-id="bc031-111">Aby skonfigurować integrację usługi Azure AD z MCM, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bc031-111">To configure Azure AD integration with MCM, you need the following items:</span></span>

- <span data-ttu-id="bc031-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc031-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bc031-113">MCM logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bc031-113">A MCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bc031-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bc031-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bc031-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bc031-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bc031-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bc031-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bc031-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc031-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bc031-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bc031-118">Scenario description</span></span>
<span data-ttu-id="bc031-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bc031-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bc031-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bc031-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc031-121">Dodawanie MCM z galerii</span><span class="sxs-lookup"><span data-stu-id="bc031-121">Adding MCM from the gallery</span></span>
2. <span data-ttu-id="bc031-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bc031-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-the-gallery"></a><span data-ttu-id="bc031-123">Dodawanie MCM z galerii</span><span class="sxs-lookup"><span data-stu-id="bc031-123">Adding MCM from the gallery</span></span>
<span data-ttu-id="bc031-124">Aby skonfigurować integrację usługi Azure AD MCM, należy dodać MCM z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bc031-124">To configure the integration of MCM into Azure AD, you need to add MCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bc031-125">**Aby dodać MCM z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bc031-125">**To add MCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bc031-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bc031-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bc031-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bc031-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bc031-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bc031-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bc031-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bc031-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bc031-133">W polu wyszukiwania wpisz **MCM**.</span><span class="sxs-lookup"><span data-stu-id="bc031-133">In the search box, type **MCM**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_search.png)

5. <span data-ttu-id="bc031-135">W panelu wyników wybierz **MCM**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bc031-135">In the results panel, select **MCM**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bc031-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bc031-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bc031-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MCM w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="bc031-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bc031-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w MCM jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc031-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MCM is to a user in Azure AD.</span></span> <span data-ttu-id="bc031-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w MCM musi się.</span><span class="sxs-lookup"><span data-stu-id="bc031-140">In other words, a link relationship between an Azure AD user and the related user in MCM needs to be established.</span></span>

<span data-ttu-id="bc031-141">W MCM, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bc031-141">In MCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bc031-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MCM, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bc031-142">To configure and test Azure AD single sign-on with MCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bc031-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bc031-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bc031-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bc031-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bc031-145">**[Użytkownik testowy tworzenie MCM](#creating-a-mcm-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta MCM połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc031-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - to have a counterpart of Britta Simon in MCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bc031-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bc031-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bc031-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bc031-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bc031-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bc031-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bc031-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji MCM.</span><span class="sxs-lookup"><span data-stu-id="bc031-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="bc031-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z MCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bc031-150">**To configure Azure AD single sign-on with MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="bc031-151">W portalu Azure na **MCM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bc031-151">In the Azure portal, on the **MCM** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bc031-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bc031-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_samlbase.png)

3. <span data-ttu-id="bc031-155">Na **MCM domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bc031-155">On the **MCM Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_url.png)

    <span data-ttu-id="bc031-157">a.</span><span class="sxs-lookup"><span data-stu-id="bc031-157">a.</span></span> <span data-ttu-id="bc031-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://myaba.co.uk/client-access/<companyname>/saml.php`</span><span class="sxs-lookup"><span data-stu-id="bc031-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span></span>

    <span data-ttu-id="bc031-159">b.</span><span class="sxs-lookup"><span data-stu-id="bc031-159">b.</span></span> <span data-ttu-id="bc031-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://myaba.co.uk/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bc031-160">In the **Identifier** textbox, type a URL using the following pattern: `https://myaba.co.uk/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bc031-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bc031-161">These values are not real.</span></span> <span data-ttu-id="bc031-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="bc031-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bc031-163">Skontaktuj się z [zespołem pomocy technicznej klienta MCM](http://mcmtechnology.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="bc031-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="bc031-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bc031-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_certificate.png) 

5. <span data-ttu-id="bc031-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bc031-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mcm-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="bc031-168">Do konfigurowania rejestracji jednokrotnej na **MCM** stronie, musisz wysłać pobrany **XML metadanych** do [MCM obsługuje zespołu](http://mcmtechnology.com/support/).</span><span class="sxs-lookup"><span data-stu-id="bc031-168">To configure single sign-on on **MCM** side, you need to send the downloaded **Metadata XML** to [MCM support team](http://mcmtechnology.com/support/).</span></span> <span data-ttu-id="bc031-169">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="bc031-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bc031-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bc031-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bc031-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bc031-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bc031-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bc031-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bc031-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc031-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="bc031-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bc031-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bc031-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bc031-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bc031-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bc031-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bc031-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bc031-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bc031-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bc031-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bc031-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bc031-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bc031-185">a.</span><span class="sxs-lookup"><span data-stu-id="bc031-185">a.</span></span> <span data-ttu-id="bc031-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bc031-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bc031-187">b.</span><span class="sxs-lookup"><span data-stu-id="bc031-187">b.</span></span> <span data-ttu-id="bc031-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bc031-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bc031-189">c.</span><span class="sxs-lookup"><span data-stu-id="bc031-189">c.</span></span> <span data-ttu-id="bc031-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bc031-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bc031-191">d.</span><span class="sxs-lookup"><span data-stu-id="bc031-191">d.</span></span> <span data-ttu-id="bc031-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bc031-192">Click **Create**.</span></span>
 
### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="bc031-193">Tworzenie użytkownika testowego MCM</span><span class="sxs-lookup"><span data-stu-id="bc031-193">Creating a MCM test user</span></span>

<span data-ttu-id="bc031-194">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w MCM.</span><span class="sxs-lookup"><span data-stu-id="bc031-194">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="bc031-195">Praca z [MCM obsługuje zespołu](http://mcmtechnology.com/support/) Aby dodać użytkowników do platformy MCM.</span><span class="sxs-lookup"><span data-stu-id="bc031-195">Work with [MCM support team](http://mcmtechnology.com/support/) to add the users in the MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="bc031-196">Możesz użyć innych MCM użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez MCM do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="bc031-196">You can use any other MCM user account creation tools or APIs provided by MCM to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bc031-197">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc031-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bc031-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu MCM.</span><span class="sxs-lookup"><span data-stu-id="bc031-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MCM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bc031-200">**Aby przypisać Simona Britta MCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bc031-200">**To assign Britta Simon to MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="bc031-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bc031-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bc031-203">Na liście aplikacji zaznacz **MCM**.</span><span class="sxs-lookup"><span data-stu-id="bc031-203">In the applications list, select **MCM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_app.png) 

3. <span data-ttu-id="bc031-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bc031-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bc031-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bc031-207">Click **Add** button.</span></span> <span data-ttu-id="bc031-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bc031-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bc031-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bc031-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bc031-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bc031-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bc031-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bc031-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bc031-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bc031-213">Testing single sign-on</span></span>

<span data-ttu-id="bc031-214">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bc031-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bc031-215">Po kliknięciu kafelka MCM w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji MCM.</span><span class="sxs-lookup"><span data-stu-id="bc031-215">When you click the MCM tile in the Access Panel, you should get automatically signed-on to your MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc031-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bc031-216">Additional resources</span></span>

* [<span data-ttu-id="bc031-217">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc031-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bc031-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bc031-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_203.png

