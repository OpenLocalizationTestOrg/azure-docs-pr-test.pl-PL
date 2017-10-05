---
title: 'Samouczek: Integracji Azure Active Directory z Nomadic | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Nomadic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 1817a1395c2ffa7268abfff268d9d041f7f21a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="e2104-103">Samouczek: Integracji Azure Active Directory z Nomadic</span><span class="sxs-lookup"><span data-stu-id="e2104-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="e2104-104">Z tego samouczka dowiesz się integrowanie Nomadic z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2104-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2104-105">Integracja z usługą Azure AD Nomadic zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e2104-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e2104-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Nomadic.</span><span class="sxs-lookup"><span data-stu-id="e2104-106">You can control in Azure AD who has access to Nomadic.</span></span>
- <span data-ttu-id="e2104-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Nomadic (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2104-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e2104-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2104-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e2104-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2104-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2104-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e2104-110">Prerequisites</span></span>

<span data-ttu-id="e2104-111">Aby skonfigurować integrację usługi Azure AD z Nomadic, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e2104-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="e2104-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2104-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2104-113">Nomadic logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e2104-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2104-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e2104-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2104-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e2104-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2104-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e2104-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2104-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2104-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2104-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e2104-118">Scenario description</span></span>
<span data-ttu-id="e2104-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e2104-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2104-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e2104-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2104-121">Dodaj Nomadic z galerii</span><span class="sxs-lookup"><span data-stu-id="e2104-121">Add Nomadic from the gallery</span></span>
2. <span data-ttu-id="e2104-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e2104-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="e2104-123">Dodaj Nomadic z galerii</span><span class="sxs-lookup"><span data-stu-id="e2104-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="e2104-124">Aby skonfigurować integrację usługi Azure AD Nomadic, należy dodać Nomadic z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e2104-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e2104-125">**Aby dodać Nomadic z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e2104-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e2104-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e2104-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="e2104-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e2104-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e2104-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e2104-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="e2104-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e2104-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="e2104-133">W polu wyszukiwania wpisz **Nomadic**, wybierz pozycję **Nomadic** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e2104-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span></span>

    ![Nomadic na liście wyników](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e2104-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e2104-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e2104-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nomadic w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e2104-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2104-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Nomadic jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2104-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="e2104-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Nomadic musi się.</span><span class="sxs-lookup"><span data-stu-id="e2104-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="e2104-139">W Nomadic, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e2104-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e2104-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nomadic, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e2104-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e2104-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e2104-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e2104-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e2104-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2104-143">**[Tworzenie użytkownika testowego Nomadic](#create-a-nomadic-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Nomadic połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e2104-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2104-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e2104-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2104-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e2104-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e2104-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e2104-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e2104-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w Nomadic aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2104-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="e2104-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Nomadic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e2104-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="e2104-149">W portalu Azure na **Nomadic** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e2104-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="e2104-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e2104-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="e2104-153">Na **Nomadic domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e2104-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny nomadic pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="e2104-155">a.</span><span class="sxs-lookup"><span data-stu-id="e2104-155">a.</span></span> <span data-ttu-id="e2104-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="e2104-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="e2104-157">b.</span><span class="sxs-lookup"><span data-stu-id="e2104-157">b.</span></span> <span data-ttu-id="e2104-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca: `https://<company name>.nomadic.fm/auth/saml2/sp`,`https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="e2104-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2104-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e2104-159">These values are not real.</span></span> <span data-ttu-id="e2104-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e2104-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e2104-161">Skontaktuj się z [zespołem pomocy technicznej klienta Nomadic](mailto:help@nomadic.fm) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e2104-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span></span> 
 


4. <span data-ttu-id="e2104-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e2104-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="e2104-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e2104-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="e2104-166">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej Nomadic](mailto:help@nomadic.fm) i udostępnia je z pobranego **metadanych**.</span><span class="sxs-lookup"><span data-stu-id="e2104-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="e2104-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e2104-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e2104-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e2104-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e2104-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2104-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e2104-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2104-170">Create an Azure AD test user</span></span>

<span data-ttu-id="e2104-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e2104-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="e2104-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e2104-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e2104-174">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e2104-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e2104-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e2104-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e2104-178">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e2104-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e2104-180">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e2104-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e2104-182">a.</span><span class="sxs-lookup"><span data-stu-id="e2104-182">a.</span></span> <span data-ttu-id="e2104-183">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2104-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2104-184">b.</span><span class="sxs-lookup"><span data-stu-id="e2104-184">b.</span></span> <span data-ttu-id="e2104-185">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e2104-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e2104-186">c.</span><span class="sxs-lookup"><span data-stu-id="e2104-186">c.</span></span> <span data-ttu-id="e2104-187">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="e2104-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e2104-188">d.</span><span class="sxs-lookup"><span data-stu-id="e2104-188">d.</span></span> <span data-ttu-id="e2104-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e2104-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="e2104-190">Tworzenie użytkownika testowego Nomadic</span><span class="sxs-lookup"><span data-stu-id="e2104-190">Create a Nomadic test user</span></span>

<span data-ttu-id="e2104-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Nomadic.</span><span class="sxs-lookup"><span data-stu-id="e2104-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="e2104-192">We współpracy z [zespołem pomocy technicznej Nomadic](mailto:help@nomadic.fm) Aby dodać użytkowników do Nomadic platformy.</span><span class="sxs-lookup"><span data-stu-id="e2104-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e2104-193">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2104-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="e2104-194">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Nomadic.</span><span class="sxs-lookup"><span data-stu-id="e2104-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="e2104-196">**Aby przypisać Simona Britta Nomadic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e2104-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="e2104-197">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e2104-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e2104-199">Na liście aplikacji zaznacz **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="e2104-199">In the applications list, select **Nomadic**.</span></span>

    ![Nomadic łącza na liście aplikacji](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="e2104-201">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e2104-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="e2104-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e2104-203">Click **Add** button.</span></span> <span data-ttu-id="e2104-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e2104-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="e2104-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e2104-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e2104-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e2104-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2104-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e2104-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e2104-209">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e2104-209">Test single sign-on</span></span>

<span data-ttu-id="e2104-210">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e2104-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e2104-211">Po kliknięciu kafelka Nomadic w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Nomadic aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2104-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>
<span data-ttu-id="e2104-212">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2104-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e2104-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e2104-213">Additional resources</span></span>

* [<span data-ttu-id="e2104-214">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2104-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2104-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e2104-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

