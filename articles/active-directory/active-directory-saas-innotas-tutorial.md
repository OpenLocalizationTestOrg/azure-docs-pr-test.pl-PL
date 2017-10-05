---
title: 'Samouczek: Integracji Azure Active Directory z Innotas | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Innotas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 674d01b2c0818dc10fdab5844a23c5ebf29bb2d2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="d01fe-103">Samouczek: Integracji Azure Active Directory z Innotas</span><span class="sxs-lookup"><span data-stu-id="d01fe-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="d01fe-104">Z tego samouczka dowiesz się integrowanie Innotas z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d01fe-104">In this tutorial, you learn how to integrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d01fe-105">Integracja z usługą Azure AD Innotas zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d01fe-105">Integrating Innotas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d01fe-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Innotas</span><span class="sxs-lookup"><span data-stu-id="d01fe-106">You can control in Azure AD who has access to Innotas</span></span>
- <span data-ttu-id="d01fe-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Innotas (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d01fe-107">You can enable your users to automatically get signed-on to Innotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d01fe-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d01fe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d01fe-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d01fe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d01fe-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d01fe-110">Prerequisites</span></span>

<span data-ttu-id="d01fe-111">Aby skonfigurować integrację usługi Azure AD z Innotas, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d01fe-111">To configure Azure AD integration with Innotas, you need the following items:</span></span>

- <span data-ttu-id="d01fe-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d01fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d01fe-113">Innotas logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d01fe-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d01fe-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d01fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d01fe-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d01fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d01fe-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d01fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d01fe-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d01fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d01fe-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d01fe-118">Scenario description</span></span>

<span data-ttu-id="d01fe-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d01fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d01fe-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d01fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d01fe-121">Dodawanie Innotas z galerii</span><span class="sxs-lookup"><span data-stu-id="d01fe-121">Adding Innotas from the gallery</span></span>
2. <span data-ttu-id="d01fe-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d01fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-the-gallery"></a><span data-ttu-id="d01fe-123">Dodawanie Innotas z galerii</span><span class="sxs-lookup"><span data-stu-id="d01fe-123">Adding Innotas from the gallery</span></span>
<span data-ttu-id="d01fe-124">Aby skonfigurować integrację usługi Azure AD Innotas, należy dodać Innotas z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d01fe-124">To configure the integration of Innotas into Azure AD, you need to add Innotas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d01fe-125">**Aby dodać Innotas z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d01fe-125">**To add Innotas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d01fe-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d01fe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d01fe-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d01fe-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d01fe-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d01fe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d01fe-133">W polu wyszukiwania wpisz **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-133">In the search box, type **Innotas**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="d01fe-135">W panelu wyników wybierz **Innotas**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d01fe-135">In the results panel, select **Innotas**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d01fe-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d01fe-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="d01fe-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Innotas na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d01fe-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d01fe-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Innotas jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d01fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Innotas is to a user in Azure AD.</span></span> <span data-ttu-id="d01fe-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Innotas musi się.</span><span class="sxs-lookup"><span data-stu-id="d01fe-140">In other words, a link relationship between an Azure AD user and the related user in Innotas needs to be established.</span></span>

<span data-ttu-id="d01fe-141">W Innotas, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="d01fe-141">In Innotas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d01fe-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Innotas, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d01fe-142">To configure and test Azure AD single sign-on with Innotas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d01fe-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d01fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d01fe-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d01fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d01fe-145">**[Tworzenie użytkownika testowego Innotas](#creating-an-innotas-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Innotas połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d01fe-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - to have a counterpart of Britta Simon in Innotas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d01fe-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d01fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d01fe-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d01fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d01fe-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d01fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d01fe-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Innotas.</span><span class="sxs-lookup"><span data-stu-id="d01fe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="d01fe-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Innotas, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d01fe-150">**To configure Azure AD single sign-on with Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="d01fe-151">W portalu Azure na **Innotas** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-151">In the Azure portal, on the **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d01fe-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d01fe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="d01fe-155">Na **Innotas domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d01fe-155">On the **Innotas Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="d01fe-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="d01fe-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d01fe-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d01fe-158">This value is not real.</span></span> <span data-ttu-id="d01fe-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="d01fe-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d01fe-160">Skontaktuj się z [zespołem pomocy technicznej klienta Innotas](https://www.innotas.com/contact) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="d01fe-160">Contact [Innotas Client support team](https://www.innotas.com/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="d01fe-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d01fe-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="d01fe-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d01fe-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d01fe-165">Do konfigurowania rejestracji jednokrotnej na **Innotas** stronie, musisz wysłać pobrany **XML metadanych** do [Innotas obsługuje zespołu](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="d01fe-165">To configure single sign-on on **Innotas** side, you need to send the downloaded **Metadata XML** to [Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="d01fe-166">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="d01fe-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d01fe-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d01fe-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d01fe-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d01fe-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d01fe-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d01fe-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d01fe-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d01fe-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="d01fe-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d01fe-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d01fe-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d01fe-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d01fe-174">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d01fe-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d01fe-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d01fe-178">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d01fe-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d01fe-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d01fe-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d01fe-182">a.</span><span class="sxs-lookup"><span data-stu-id="d01fe-182">a.</span></span> <span data-ttu-id="d01fe-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d01fe-184">b.</span><span class="sxs-lookup"><span data-stu-id="d01fe-184">b.</span></span> <span data-ttu-id="d01fe-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d01fe-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d01fe-186">c.</span><span class="sxs-lookup"><span data-stu-id="d01fe-186">c.</span></span> <span data-ttu-id="d01fe-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d01fe-188">d.</span><span class="sxs-lookup"><span data-stu-id="d01fe-188">d.</span></span> <span data-ttu-id="d01fe-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="d01fe-190">Tworzenie użytkownika testowego Innotas</span><span class="sxs-lookup"><span data-stu-id="d01fe-190">Creating an Innotas test user</span></span>

<span data-ttu-id="d01fe-191">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej Innotas użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d01fe-191">There is no action item for you to configure user provisioning to Innotas.</span></span>  
<span data-ttu-id="d01fe-192">Gdy przypisany użytkownik próbuje zalogować się do Innotas za pomocą panelu dostępu, Innotas sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="d01fe-192">When an assigned user tries to log in to Innotas using the access panel, Innotas checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="d01fe-193">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Innotas.</span><span class="sxs-lookup"><span data-stu-id="d01fe-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d01fe-194">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d01fe-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d01fe-195">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Innotas.</span><span class="sxs-lookup"><span data-stu-id="d01fe-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innotas.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d01fe-197">**Aby przypisać Simona Britta Innotas, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d01fe-197">**To assign Britta Simon to Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="d01fe-198">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d01fe-200">Na liście aplikacji zaznacz **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-200">In the applications list, select **Innotas**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="d01fe-202">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d01fe-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d01fe-204">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d01fe-204">Click **Add** button.</span></span> <span data-ttu-id="d01fe-205">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d01fe-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d01fe-207">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d01fe-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d01fe-208">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d01fe-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d01fe-209">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d01fe-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d01fe-210">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d01fe-210">Testing single sign-on</span></span>

<span data-ttu-id="d01fe-211">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d01fe-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d01fe-212">Po kliknięciu kafelka Innotas w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Innotas.</span><span class="sxs-lookup"><span data-stu-id="d01fe-212">When you click the Innotas tile in the Access Panel, you should get automatically signed-on to your Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d01fe-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d01fe-213">Additional resources</span></span>

* [<span data-ttu-id="d01fe-214">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d01fe-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d01fe-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d01fe-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

