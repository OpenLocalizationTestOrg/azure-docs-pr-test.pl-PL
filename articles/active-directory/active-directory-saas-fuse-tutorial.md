---
title: 'Samouczek: Integracji Azure Active Directory z bezpiecznik | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i bezpiecznik."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="65581-103">Samouczek: Integracji Azure Active Directory z bezpiecznik</span><span class="sxs-lookup"><span data-stu-id="65581-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="65581-104">W tym samouczku Dowiedz się jak zintegrować bezpiecznik w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65581-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65581-105">Integracja z usługą Azure AD bezpiecznik zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="65581-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65581-106">Można kontrolować w usłudze Azure AD, który ma dostęp do bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="65581-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="65581-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do bezpiecznik (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65581-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65581-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65581-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="65581-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65581-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65581-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="65581-110">Prerequisites</span></span>

<span data-ttu-id="65581-111">Aby skonfigurować integrację usługi Azure AD z bezpiecznik, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="65581-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="65581-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65581-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65581-113">Bezpiecznik logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="65581-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65581-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="65581-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65581-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="65581-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65581-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="65581-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65581-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65581-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65581-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="65581-118">Scenario description</span></span>
<span data-ttu-id="65581-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="65581-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65581-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="65581-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65581-121">Dodaj bezpiecznik z galerii</span><span class="sxs-lookup"><span data-stu-id="65581-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="65581-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65581-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="65581-123">Dodaj bezpiecznik z galerii</span><span class="sxs-lookup"><span data-stu-id="65581-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="65581-124">Aby skonfigurować integrację usługi Azure AD bezpiecznik, należy dodać bezpiecznik z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="65581-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65581-125">**Aby dodać bezpiecznik z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="65581-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65581-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="65581-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="65581-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="65581-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65581-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="65581-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="65581-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65581-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="65581-133">W polu wyszukiwania wpisz **łączenie**, wybierz pozycję **łączenie** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="65581-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Łączenie z listy wyników](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65581-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65581-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="65581-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z bezpiecznik w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="65581-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65581-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w bezpiecznik jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65581-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="65581-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w bezpiecznik musi się.</span><span class="sxs-lookup"><span data-stu-id="65581-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="65581-139">W bezpiecznik, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="65581-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65581-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z bezpiecznik, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="65581-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65581-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="65581-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65581-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="65581-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65581-143">**[Tworzenie użytkownika testowego bezpiecznik](#create-a-fuse-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta bezpiecznik połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65581-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65581-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="65581-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65581-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="65581-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65581-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65581-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65581-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="65581-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="65581-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z bezpiecznik, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="65581-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="65581-149">W portalu Azure na **łączenie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="65581-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="65581-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="65581-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="65581-153">Na **adresy URL i łączenie domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="65581-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Łączenie domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="65581-155">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="65581-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65581-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="65581-156">This value is not real.</span></span> <span data-ttu-id="65581-157">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="65581-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="65581-158">Skontaktuj się z [zespołem pomocy technicznej klienta łączenie](mailto:support@fusion-universal.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="65581-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="65581-159">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="65581-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="65581-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65581-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65581-163">Na **łączenie konfiguracji** kliknij **skonfigurować łączenie** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="65581-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65581-164">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="65581-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Łączenie konfiguracji](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="65581-166">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej bezpiecznik](mailto:support@fusion-universal.com) i podaj następujące:</span><span class="sxs-lookup"><span data-stu-id="65581-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="65581-167">Pobrany **plik certyfikatu (Raw)**</span><span class="sxs-lookup"><span data-stu-id="65581-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="65581-168">**Adres URL usługi rejestracji jednokrotnej SAML**</span><span class="sxs-lookup"><span data-stu-id="65581-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="65581-169">**Identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="65581-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="65581-170">**Adresu URL wylogowania**</span><span class="sxs-lookup"><span data-stu-id="65581-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="65581-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="65581-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65581-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="65581-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65581-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65581-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65581-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65581-174">Create an Azure AD test user</span></span>

<span data-ttu-id="65581-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="65581-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="65581-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="65581-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65581-178">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65581-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="65581-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="65581-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="65581-182">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="65581-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="65581-184">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="65581-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="65581-186">a.</span><span class="sxs-lookup"><span data-stu-id="65581-186">a.</span></span> <span data-ttu-id="65581-187">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65581-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65581-188">b.</span><span class="sxs-lookup"><span data-stu-id="65581-188">b.</span></span> <span data-ttu-id="65581-189">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="65581-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="65581-190">c.</span><span class="sxs-lookup"><span data-stu-id="65581-190">c.</span></span> <span data-ttu-id="65581-191">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="65581-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="65581-192">d.</span><span class="sxs-lookup"><span data-stu-id="65581-192">d.</span></span> <span data-ttu-id="65581-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="65581-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="65581-194">Tworzenie użytkownika testowego bezpiecznik</span><span class="sxs-lookup"><span data-stu-id="65581-194">Create a Fuse test user</span></span>

<span data-ttu-id="65581-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="65581-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="65581-196">We współpracy z [zespołem pomocy technicznej bezpiecznik](mailto:support@fusion-universal.com) Aby dodać użytkowników do platformy bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="65581-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="65581-197">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65581-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="65581-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="65581-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="65581-200">**Aby przypisać Simona Britta bezpiecznik, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="65581-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="65581-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="65581-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="65581-203">Na liście aplikacji zaznacz **łączenie**.</span><span class="sxs-lookup"><span data-stu-id="65581-203">In the applications list, select **Fuse**.</span></span>

    ![Łącze bezpiecznik na liście aplikacji](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="65581-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="65581-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="65581-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65581-207">Click **Add** button.</span></span> <span data-ttu-id="65581-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65581-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="65581-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="65581-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65581-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65581-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65581-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65581-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65581-213">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65581-213">Test single sign-on</span></span>

<span data-ttu-id="65581-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="65581-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65581-215">Po kliknięciu kafelka bezpiecznik w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="65581-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="65581-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65581-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65581-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="65581-217">Additional resources</span></span>

* [<span data-ttu-id="65581-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65581-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65581-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65581-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

