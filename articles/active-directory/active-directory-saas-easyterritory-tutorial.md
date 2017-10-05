---
title: 'Samouczek: Integracji Azure Active Directory z EasyTerritory | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i EasyTerritory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 46f99496397e2ed39b1d9410453dac7983ced612
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="e9761-103">Samouczek: Integracji Azure Active Directory z EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="e9761-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="e9761-104">Z tego samouczka dowiesz się integrowanie EasyTerritory z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9761-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9761-105">Integracja z usługą Azure AD EasyTerritory zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e9761-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9761-106">Można kontrolować w usłudze Azure AD, który ma dostęp do EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="e9761-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="e9761-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do EasyTerritory (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9761-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e9761-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e9761-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e9761-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9761-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9761-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e9761-110">Prerequisites</span></span>

<span data-ttu-id="e9761-111">Aby skonfigurować integrację usługi Azure AD z EasyTerritory, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e9761-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="e9761-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9761-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9761-113">EasyTerritory jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e9761-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9761-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e9761-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9761-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e9761-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9761-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e9761-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9761-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9761-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9761-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e9761-118">Scenario description</span></span>
<span data-ttu-id="e9761-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e9761-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9761-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e9761-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9761-121">Dodawanie EasyTerritory z galerii</span><span class="sxs-lookup"><span data-stu-id="e9761-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="e9761-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e9761-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="e9761-123">Dodawanie EasyTerritory z galerii</span><span class="sxs-lookup"><span data-stu-id="e9761-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="e9761-124">Aby skonfigurować integrację usługi Azure AD EasyTerritory, należy dodać EasyTerritory z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e9761-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9761-125">**Aby dodać EasyTerritory z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e9761-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9761-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e9761-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="e9761-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e9761-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9761-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e9761-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="e9761-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9761-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="e9761-133">W polu wyszukiwania wpisz **EasyTerritory**, wybierz pozycję **EasyTerritory** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e9761-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![EasyTerritory na liście wyników](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e9761-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9761-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e9761-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z EasyTerritory w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e9761-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9761-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w EasyTerritory jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9761-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="e9761-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w EasyTerritory musi się.</span><span class="sxs-lookup"><span data-stu-id="e9761-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="e9761-139">W EasyTerritory, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e9761-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e9761-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z EasyTerritory, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e9761-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9761-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e9761-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9761-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e9761-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9761-143">**[Tworzenie użytkownika testowego EasyTerritory](#create-a-easyterritory-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta EasyTerritory połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9761-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9761-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e9761-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9761-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e9761-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e9761-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9761-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e9761-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="e9761-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="e9761-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z EasyTerritory, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e9761-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="e9761-149">W portalu Azure na **EasyTerritory** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e9761-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="e9761-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e9761-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="e9761-153">Na **EasyTerritory domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w trybie IDP inicjowane:</span><span class="sxs-lookup"><span data-stu-id="e9761-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Adresy URL i domeny EasyTerritory pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="e9761-155">a.</span><span class="sxs-lookup"><span data-stu-id="e9761-155">a.</span></span> <span data-ttu-id="e9761-156">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="e9761-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="e9761-157">b.</span><span class="sxs-lookup"><span data-stu-id="e9761-157">b.</span></span> <span data-ttu-id="e9761-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="e9761-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="e9761-159">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonać następujący krok, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="e9761-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Adresy URL i domeny EasyTerritory pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="e9761-161">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="e9761-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e9761-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e9761-162">These values are not real.</span></span> <span data-ttu-id="e9761-163">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e9761-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e9761-164">Skontaktuj się z [zespołem pomocy technicznej klienta EasyTerritory](mailto:sales@easyterritory.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e9761-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

5. <span data-ttu-id="e9761-165">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e9761-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="e9761-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9761-167">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e9761-169">Skonfigurować logowanie jednokrotne w **EasyTerritory** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="e9761-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="e9761-170">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="e9761-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e9761-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e9761-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e9761-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e9761-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e9761-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9761-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e9761-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9761-174">Create an Azure AD test user</span></span>

<span data-ttu-id="e9761-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e9761-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="e9761-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e9761-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9761-178">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9761-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e9761-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e9761-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e9761-182">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e9761-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e9761-184">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e9761-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e9761-186">a.</span><span class="sxs-lookup"><span data-stu-id="e9761-186">a.</span></span> <span data-ttu-id="e9761-187">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9761-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9761-188">b.</span><span class="sxs-lookup"><span data-stu-id="e9761-188">b.</span></span> <span data-ttu-id="e9761-189">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e9761-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e9761-190">c.</span><span class="sxs-lookup"><span data-stu-id="e9761-190">c.</span></span> <span data-ttu-id="e9761-191">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="e9761-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e9761-192">d.</span><span class="sxs-lookup"><span data-stu-id="e9761-192">d.</span></span> <span data-ttu-id="e9761-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e9761-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="e9761-194">Tworzenie użytkownika testowego EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="e9761-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="e9761-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="e9761-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="e9761-196">We współpracy z [zespołem pomocy technicznej EasyTerritory](mailto:sales@easyterritory.com) Aby dodać użytkowników do platformy EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="e9761-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e9761-197">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9761-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="e9761-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="e9761-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="e9761-200">**Aby przypisać Simona Britta EasyTerritory, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e9761-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="e9761-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e9761-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e9761-203">Na liście aplikacji zaznacz **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="e9761-203">In the applications list, select **EasyTerritory**.</span></span>

    ![Łącze EasyTerritory na liście aplikacji](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="e9761-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e9761-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="e9761-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9761-207">Click **Add** button.</span></span> <span data-ttu-id="e9761-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9761-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="e9761-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e9761-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9761-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9761-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9761-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9761-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e9761-213">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9761-213">Test single sign-on</span></span>

<span data-ttu-id="e9761-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e9761-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9761-215">Po kliknięciu kafelka EasyTerritory w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="e9761-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="e9761-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9761-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9761-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e9761-217">Additional resources</span></span>

* [<span data-ttu-id="e9761-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9761-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9761-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9761-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

